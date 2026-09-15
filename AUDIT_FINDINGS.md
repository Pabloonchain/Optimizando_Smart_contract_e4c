# 🛡️ Reporte de Auditoría de Seguridad: Smart Contracts E4C (Stellar / Soroban)

**Proyecto:** E4C (Educación, Reconocimiento Escolar y Tokenómica Cultural Dual)  
**Entorno de Ejecución:** Stellar Network (Soroban Rust SDK v22.0.0+)  
**Objetivo de la Auditoría:** Detección de vulnerabilidades, optimización de almacenamiento en ledger, gestión de ciclo de vida (TTL), control de acceso y mitigación de vectores de denegación de servicio (DoS) para presentación y defensa en Hackathon.

---

## 📊 1. Resumen Ejecutivo de Hallazgos

| ID | Título de la Vulnerabilidad | Severidad | Contrato Afectado | Estado |
|---|---|---|---|---|
| **E4C-SEC-01** | Agotamiento de Límite de Storage de Instancia (64KB DoS) | 🔴 **CRÍTICA** | `edu_validator`, `token_swap`, `partner_escrow` | ✅ **RESUELTO** |
| **E4C-SEC-02** | Control de Acceso Roto en Emisión de Tokens (`mint_e4c`) | 🔴 **CRÍTICA** | `token_swap` | ✅ **RESUELTO** |
| **E4C-SEC-03** | DoS por Archivado de Estado no Renovado (Falta de `extend_ttl`) | 🟠 **ALTA** | Todos los contratos (`edu_validator`, `token_swap`, `partner_escrow`, `edu-account`) | ✅ **RESUELTO** |
| **E4C-SEC-04** | Manejo de Errores con Pánico en lugar de Códigos Estructurados | 🟡 **MEDIA** | `partner_escrow` | ✅ **RESUELTO** |
| **E4C-SEC-05** | Ambigüedad Criptográfica en Smart Account (Passkey vs Ed25519) | 🟡 **MEDIA** | `edu-account` | ✅ **RESUELTO** |
| **E4C-SEC-06** | Cobertura Nula de Pruebas Unitarias en Flujos de Canje y Cuentas | 🟡 **MEDIA** | `token_swap`, `edu-account` | ✅ **RESUELTO** |
| **E4C-SEC-07** | Inicialización Expuesta sin Constructor Atómico | 🔵 **BAJA** | Todos los contratos | ℹ️ **MITIGADO** |

---

## 🔎 2. Detalle Técnico de Vulnerabilidades

---

### 🔴 E4C-SEC-01: Agotamiento de Límite de Storage de Instancia (64KB DoS)
- **Severidad:** Crítica (CWE-400: Uncontrolled Resource Consumption)
- **Archivos Afectados:**
  - `contracts/edu_validator/src/lib.rs` (L153, L186, L276)
  - `contracts/token_swap/src/lib.rs` (L183)
  - `contracts/partner_escrow/src/lib.rs` (L100, L135)

#### Descripción del Problema
En el modelo de almacenamiento de Soroban, `env.storage().instance()` comparte **una única entrada de ledger para todo el contrato, limitada estrictamente a 64 KB serializados**.
Actualmente, los contratos almacenan colecciones que crecen de manera ilimitada con el uso de los alumnos dentro de `instance()`:
1. En `edu_validator`:
   ```rust
   // ⚠️ VULNERABLE: Se almacena en instance() por cada alumno y por cada desafío
   let challenge_key = DataKey::StudentChallenge(student.clone(), challenge_id);
   env.storage().instance().set(&challenge_key, &true);

   // ⚠️ VULNERABLE: Registro de asistencia diaria de cada alumno en instance()
   let att_key = DataKey::StudentAttendance(student.clone(), subject_id, current_day);
   env.storage().instance().set(&att_key, &true);
   ```
2. En `token_swap`:
   ```rust
   // ⚠️ VULNERABLE: Cada ticket cultural canjeado agrega un struct a instance()
   env.storage().instance().set(&DataKey::Voucher(nonce), &voucher);
   ```
3. En `partner_escrow`:
   ```rust
   // ⚠️ VULNERABLE: Cada pasaporte de estudiante con su Vec dinámico en instance()
   env.storage().instance().set(&DataKey::StudentPassport(student.clone()), &passport);
   ```

#### Impacto
A medida que decenas de alumnos completen tareas, registren presentismo diario y canjeen pases culturales, el tamaño de la instancia superará rápidamente los 64 KB. Al ocurrir esto, **el host de Soroban rechazará cualquier transacción que intente leer o escribir en la instancia, dejando el contrato permanentemente inoperativo (bricked)**.

#### Remediación
- Migrar todas las entradas por alumno/por ticket a `env.storage().persistent()`.
- Para datos efímeros como la cuota diaria profesor-alumno (`StudentTeacherMint`), migrar a `env.storage().temporary()` ya que solo tiene validez durante el día en curso.
- Mantener en `instance()` únicamente configuraciones inmutables de bajo tamaño (`Admin`, direcciones de tokens SAC).

---

### 🔴 E4C-SEC-02: Control de Acceso Roto en Emisión de Tokens (`mint_e4c`)
- **Severidad:** Crítica (CWE-285: Improper Authorization)
- **Archivo Afectado:** `contracts/token_swap/src/lib.rs` (L97-L127)

#### Descripción del Problema
El método `mint_e4c` en el contrato `token_swap` fue concebido para transferir tokens $E4C desde la reserva del contrato hacia un estudiante:

```rust
pub fn mint_e4c(
    env: Env,
    teacher: Address,
    student: Address,
    amount: i128,
) -> Result<(), SwapError> {
    teacher.require_auth(); // ⚠️ SOLO valida que quien llama sea dueño de 'teacher'

    if amount <= 0 || amount > 40 {
        return Err(SwapError::InvalidAmount);
    }

    let e4c_token: Address = env.storage().instance().get(&DataKey::E4cToken)...;
    let e4c_client = token::Client::new(&env, &e4c_token);
    let contract_address = env.current_contract_address();
    
    // Transfiere tokens desde el contrato al estudiante sin validar rol docente
    e4c_client.transfer(&contract_address, &student, &amount);
    Ok(())
}
```

#### Impacto
Cualquier usuario arbitrario puede invocar `mint_e4c` firmando con su propia cuenta (`teacher = atacante`). Como la función únicamente llama a `teacher.require_auth()`, **la firma es válida**, pero el contrato **nunca verifica si `teacher` está en una lista de docentes registrados**. Un atacante puede llamar repetidamente a esta función y drenar el saldo de $E4C del contrato hacia sus propias cuentas.

#### Remediación
1. El contrato `token_swap` está diseñado para el intercambio y quema de pases culturales ($E4C \rightarrow $ACT $\rightarrow$ Ticket Taquilla). La emisión pedagógica legítima ya se encuentra regulada y protegida en `edu_validator` con cuotas diarias docentes y mitigación de colusión.
2. Por lo tanto, `mint_e4c` debe ser eliminado de `token_swap`, o bien restringido exclusivamente a la firma del `Admin` institucional.

---

### 🟠 E4C-SEC-03: DoS por Archivado de Estado no Renovado (Falta de `extend_ttl`)
- **Severidad:** Alta (CWE-770: Allocation of Resources Without Limits or Throttling)
- **Archivos Afectados:** Todos los contratos en `/contracts`.

#### Descripción del Problema
En el modelo de renta de almacenamiento de Stellar Soroban (Protocolo 20+), cada entrada en el ledger tiene un tiempo de vida (TTL) medido en ledgers (~5 segundos por ledger, 17.280 ledgers por día).
Si una entrada no es extendida (`extend_ttl`), entra en estado archivado tras ~120 a 180 días. Ninguno de los contratos implementa renovación de TTL.

#### Impacto
Si el contrato o las credenciales de un estudiante pasan un período de vacaciones o inactividad prolongada sin llamadas, el contrato quedará archivado. Las transacciones posteriores fallarán automáticamente en la simulación a menos que el cliente declare un footprint de restauración con pago de renta.

#### Remediación
Implementar rutinas automáticas de extensión de TTL con umbrales estándar de la red:
```rust
const DAY_IN_LEDGERS: u32 = 17280;
const BUMP_THRESHOLD: u32 = 30 * DAY_IN_LEDGERS; // Si restan menos de 30 días
const BUMP_TO: u32 = 120 * DAY_IN_LEDGERS;       // Renovar a 120 días

env.storage().instance().extend_ttl(BUMP_THRESHOLD, BUMP_TO);
```

---

### 🟡 E4C-SEC-04: Manejo de Errores con Pánico en lugar de Códigos Estructurados
- **Severidad:** Media (CWE-390: Detection of Error Condition Without Action)
- **Archivo Afectado:** `contracts/partner_escrow/src/lib.rs` (L28, L37, L56, L64, L67)

#### Descripción del Problema
`partner_escrow` utiliza macros `panic!("already initialized")` y `.expect("not initialized")`.

#### Impacto
Cuando una llamada falla por pánico, la máquina virtual de Soroban emite un error genérico de ejecución de host (`HostError`). Esto impide que las aplicaciones web, los SDKs de frontend (`@stellar/stellar-sdk`) o las interfaces de usuario capturen un código de error semántico para mostrar notificaciones legibles al docente o estudiante.

#### Remediación
Definir un enum `#[contracterror]` con representación numérica (`#[repr(u32)]`) y hacer que las funciones retornen `Result<T, EscrowError>`.

---

### 🟡 E4C-SEC-05: Ambigüedad Criptográfica en Smart Account (Passkey vs Ed25519)
- **Severidad:** Media (CWE-347: Improper Verification of Cryptographic Signature)
- **Archivo Afectado:** `contracts/edu-account/src/lib.rs` (L21, L33, L102)

#### Descripción del Problema
El contrato implementa `CustomAccountInterface` para Abstracción de Cuenta. La variable se nombra `passkey_id: BytesN<32>`, pero la verificación se realiza con:
```rust
env.crypto().ed25519_verify(&passkey_id, &payload_bytes, &signature);
```
Las credenciales Passkey nativas de navegadores y dispositivos móviles (WebAuthn / FIDO2 / Secure Enclave) operan sobre la curva NIST **secp256r1 (P-256)** o RSA, produciendo firmas de 64 bytes que no son compatibles con `ed25519_verify`.

#### Impacto
Una aplicación cliente que intente autenticar mediante WebAuthn nativo del navegador no podrá validar sus firmas.

#### Remediación
- Si el contrato está destinado a delegación de firmas con pares de claves estándar de Stellar, documentar y renombrar formalmente a `signer_key` / `Ed25519`.
- Si se persigue el soporte estricto de Passkeys WebAuthn, utilizar `env.crypto().secp256r1_verify(...)` pasando las coordenadas de la clave pública P-256.

---

### 🟡 E4C-SEC-06: Cobertura Nula de Pruebas Unitarias en Flujos de Canje y Cuentas
- **Severidad:** Media (CWE-1077: Floating Point Comparison Issues / Untested Paths)
- **Archivos Afectados:** `contracts/token_swap`, `contracts/edu-account`.

#### Descripción del Problema
`contracts/token_swap` y `contracts/edu-account` carecen de módulos de tests unitarios (`#[cfg(test)]`).

#### Impacto
Cualquier cambio de lógica en el canje dual de tokens $E4C $\rightarrow$ $ACT $\rightarrow$ Ticket o en la verificación de firmas puede introducir regresiones silenciosas antes del despliegue en Testnet/Mainnet.

#### Remediación
Implementar tests unitarios completos simulando el entorno con `soroban_sdk::Env`, clientes de token SAC y aserciones de éxito y error.

---

### 🔵 E4C-SEC-07: Inicialización Expuesta sin Constructor Atómico
- **Severidad:** Baja (CWE-665: Improper Initialization)
- **Archivos Afectados:** Todos los contratos que utilizan `pub fn initialize(...)`.

#### Descripción del Problema
Los contratos utilizan un método público `initialize` protegido con flags en almacenamiento. Aunque previene la reinicialización una vez ejecutado, existe una pequeña ventana de tiempo entre el despliegue del bytecode y la invocación de `initialize` donde un observador del mempool podría anticipar la llamada.

#### Remediación
Adoptar el constructor nativo de Soroban `pub fn __constructor(env: Env, ...)` que se ejecuta de forma indivisible y atómica al momento de instanciar el contrato en la red.
