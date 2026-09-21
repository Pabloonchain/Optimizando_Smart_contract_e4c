# 📘 Manual de Usuario Oficial — E4C (Education 4 Culture)

---

## 1. Portada e Información Documental

| Atributo | Detalle |
| :--- | :--- |
| **Aplicación** | **E4C — Education 4 Culture (Stellar Edition)** |
| **Versión del Sistema** | **v1.62 (Rumbo a Producción)** |
| **Fecha de Actualización** | **Septiembre 2026** |
| **Equipo / Autor** | **E4C Core Development Team** |
| **Contacto de Soporte** | `soporte@e4c.education` |
| **Ambiente de Red** | **Stellar Mainnet / Testnet** & Supabase Cloud |

### 📜 Historial de Cambios y Versiones

| Versión | Fecha | Resumen de Novedades e Hitos Principales |
| :--- | :--- | :--- |
| **v1.62** | Sep 2026 | **Rumbo a Producción — Tutor Socrático Accesible, ABM Docente de Alumnos, Respuestas Separadas en Panel de Corrección, Catálogo de Desafíos y Resiliencia en Asistencia**: (1) **Reingeniería Pedagógica del Tutor Socrático (`aiService.ts`, `generate-ai-evaluation` & `SocraticEvaluationModal.tsx`)**: Cada repregunta incorpora una introducción empática obligatoria explicando el **por qué** de la pregunta y vinculándola explícitamente al tema del desafío (`«taskTitle»`). Se erradica la jerga filosófica abstracta por lenguaje accesible y cotidiano para estudiantes de secundaria, con renderizado formateado de párrafos y etiquetas clave en cian (`💡 ¿Por qué te pregunto esto?` vs `👉 Tu pregunta:`). Calibración de rúbrica de 3 niveles ante respuestas básicas (<20 palabras), intermedias (20-55 palabras) y avanzadas (>55 palabras) sin elogios falsos. (2) **Desglose de Respuestas Socráticas en Panel Docente (`TaskReview.tsx`)**: Presentación individualizada y numerada de cada intervención del alumno (`Respuesta 1`, `Respuesta 2`, etc.), con badges de fase, preguntas de Eduki y formato de párrafo espaciado para corrección ágil. (3) **Panel Docente de ABM de Alumnos (`TeacherStudentApproval.tsx` & `TeacherDashboard.tsx`)**: Sub-pestaña `[ABM de Alumnos]` con autonomía completa docente para aprobar solicitudes de ingreso (con billetera y trustline automáticos), modificar nombres y datos de estudiantes mediante modal interactivo y dar de baja alumnos con eliminación en cascada. Atajo inteligente en `TaskAssignment.tsx`. (4) **Catálogo y Eliminación en Cascada de Desafíos Subidos (`TeacherUploadedTasks.tsx`)**: Auditoría completa de consignas creadas por el docente con filtros de curso y división, y eliminación en cascada con modal de confirmación pedagógica. (5) **Resiliencia en Toma de Asistencia y Visor de Partes Anteriores (`DailyAttendanceModule.tsx`)**: Persistencia multi-nivel garantizada (`localStorage` + Supabase + Soroban) y barra superior de partes históricos registrados. |
| **v1.61** | Sep 2026 | **Auditoría Integral de Seguridad Stellar Soroban, Reingeniería de Cupones Culturales, Persistencia Multi-Nivel y UX Sin Fricción**: (1) **Auditoría de Smart Contracts Soroban (Hackathon Ready)**: Remediación de Storage de Instancia (64KB DoS - `E4C-SEC-01`) migrando colecciones a `persistent()` y renta cero con `temporary()`; blindaje de control de acceso erradicando `mint_e4c` de `token_swap` (`E4C-SEC-02`); extensiones proactivas de TTL (`E4C-SEC-03`); manejo de errores tipados `EscrowError` (`E4C-SEC-04`); clarificación criptográfica `SignerKey` (`E4C-SEC-05`); y suites completas de tests unitarios `#[cfg(test)]` (`E4C-SEC-06`). Reportes oficiales en [`AUDIT_FINDINGS.md`](contracts/AUDIT_FINDINGS.md) y [`AUDIT_IMPROVEMENTS.md`](contracts/AUDIT_IMPROVEMENTS.md). (2) **Reingeniería de Cupones Culturales y Marketplace Estudiantil (`Marketplace.tsx`)**: Switcher dual de pestañas en cabecera `[🎭 Explorar Catálogo]` vs `[🎟️ Mis Cupones Adquiridos]`; barra banner de acceso rápido `[📱 Ver QR / Pase]` sin scroll; erradicación de secciones sepultadas al fondo; priorización estricta de activos sobre consumidos y filtros por píldoras. (3) **Persistencia Multi-Nivel y Normalización de Vouchers**: Corrección de incompatibilidad UUID en Supabase (`redeems.id` tipo UUID; código Soroban en `voucher_uuid`), recuperación híbrida y desduplicada combinando `localStorage` y Supabase (`tokenSwapService.getStudentVouchers`), y soporte dual de lectura en la Terminal Web POS (`/pos`). (4) **Estabilidad Visual y Prevención de Ciclos de Re-renderizado**: Erradicación del bucle infinito entre `rewards` y `fetchRedeemHistory` con `rewardsRef`, y supresión de clases `animate-pulse` y `animate-ping` parpadeantes. (5) **Navegación Sin Recargas Involuntarias (No-Flicker Navigation)**: Preservación de UI con `isViewingExistingVoucher` al cerrar el modal de QR y confinamiento del esqueleto de carga de pantalla completa con `hasLoadedStudentRef` en `StudentDashboard.tsx`. (6) **Generación Táctil de Avatar con Auto-Scroll y Foco**: Acceso directo desde la tarjeta de perfil escolar con mensaje interactivo *"Sin avatar, presioná acá para crearlo"*, desplazamiento suave centrado y foco automático en el prompt. (7) **Auto-Minimizado de Eduki Guía Docente**: Minimizado automático del asistente al autogenerar y cargar tareas en el formulario principal (`TaskAssignment.tsx`). (8) **Micro-Learning Docente Bloqueado**: Estado "Próximamente" en cápsulas de video en preproducción de la Guía de Bolsillo (`TeacherPocketGuide.tsx`). |
| **v1.6** | Sep 2026 | **Adopción Táctica en Aula, Kits Turnkey Curriculares, Guía de Bolsillo, Marketplace Docente, Continuidad Pedagógica, Cero Latencia Socrática y Gobernanza Directiva**: Lanzamiento de la biblioteca de secuencias didácticas socráticas listas para ejecutar (`curriculumTemplates.ts`) para Física, Química, Matemática, Lengua y Formación Ética, alineadas a la NES / Secundaria Aprende (CABA / PBA). Calibración dialéctica del Tutor Eduki con trampas cognitivas y contraejemplos epistémicos (aceleración gravitatoria en cúspide, minimización energética molecular, contraejemplo numérico pitagórico). Generador y exportador de **Secuencia Didáctica Oficial en 1 Carilla** (`SocraticRubricPDF.tsx`) con membrete del Ministerio de Educación CABA, secuencia de 60 minutos y rúbrica de 3 niveles (*Inicial*, *En Proceso*, *Logrado*). **Guía de Bolsillo Low-Touch** (`TeacherPocketGuide.tsx`) con comandos de voz estandarizados, carrusel de micro-learning y enlace dinámico directo a WhatsApp (`+54 9 11 2634-8727`). **Diploma de Reconocimiento y Alineación Pedagógica Docente** (`TeacherCertificateView.tsx`) como distinción institucional de adhesión y perseverancia frente al curso (sin horas cátedra oficiales estatutarias). **Sistema de Recompensa Docente por Perseverancia (+1 E4C por cada desafío completado y validado de sus alumnos)** y **Marketplace Cultural Docente** (`TeacherMarketplaceView.tsx`) con canje de vouchers en libros pedagógicos (FCE), pases teatrales (CTBA), ciclos de cine debate (Gaumont) y cafés literarios. Desbloqueo de salidas colectivas por gamificación inversa (Planetario Galileo Galilei, Cine Gaumont o CTBA) con $\ge 85\%$ de presentismo y $\ge 75\%$ de aprobación. **Dashboard Ejecutivo Directivo** (`ExecutiveDirectorDashboard.tsx`) con semáforo normativo de ausentismo crónico (Reglamento Escolar CABA Art. 83 bis) y KPIs ejecutivos de impacto pedagógico y cultural. Integración en **Eduki Guía** (`AIAssistant.tsx`) de **Guías Pedagógicas Low-Touch Instantáneas** (Régimen Académico CABA Res. N° 223/MEDGC/26, Dinámicas Socráticas de Debate y Detección Formativa Anti-Copia de IA) con respuesta de cero latencia, y soporte desacoplado de la acción `pedagogical_guidance` en la Edge Function `generate-ai-evaluation` y `aiService.ts` para consultas docentes abiertas en lenguaje natural. **Motor de Continuidad Pedagógica y Avance Continuo (Res. N° 223/MEDGC/26)**: Auditoría reactiva del historial de desafíos de la materia y curso con escalabilidad cognitiva de Zona de Desarrollo Próximo (Desafío inicial $\rightarrow$ TP $\rightarrow$ Evaluación Integral / ABP), diagnóstico de trayectoria y generación en 1 toque del desafío siguiente en dificultad o inicio de secuencia fundacional. **Motor Socrático de Cero Latencia y Detección Inmediata de Copia IA / Pegado (`SocraticEvaluationModal.tsx` & `aiCopyDetector.ts`)**: Apertura instantánea (0ms) en Fase 1 sin spinners de carga iniciales prematuros (`getInstantOpeningQuestion`), captura de eventos de pegado de portapapeles (`onPaste`) y evaluación local instantánea (0ms) con rechazo automático de contenido generado por IA sin demoras de red. |
| **v1.56** | Sep 2026 | **Selector Universal de Perfiles Institucionales, Blindaje de Navegación Multi-Rol y Acceso Permanente a Cierre de Sesión**: Implementación del **Selector Desplegable de Perfiles** (`Navigation.tsx`) para administradores (`[ 🛡️ Perfil Activo: Admin (7 roles) ▼ ]`) visible de forma permanente e incondicional en todas las resoluciones (móvil, tablet y escritorio). Centraliza el acceso y conmutación entre los **7 roles oficiales** de la plataforma: Admin, Docente, Preceptor, Estudiante, Validador, Ranking y Gobierno, cada uno con descripciones pedagógicas, iconos vectoriales, tilde activa y botón directo de cierre de sesión. Incorporación formal del perfil **Validador** (`validator`) a la barra de navegación superior. Reingeniería de la barra en 3 bloques estructurales desacoplados (Marca E4C / Selector / Acciones) con anclaje fijo (`shrink-0`) para la Terminal POS Taquilla, Ayuda y Cerrar Sesión («Salir»), erradicando de raíz cualquier desbordamiento horizontal (`overflow-x-auto`) o recorte visual de botones en pantallas estándar o escaladas. Detección multicapa y resiliente de privilegios administrativos (`isAdmin`) cruzando rol activo, rol original, metadatos y padrón `allAdmins` para preservar la capacidad de conmutación sin pérdida de permisos. Depuración de componentes huérfanos (`AuthStatus`) en cabecera y en `App.tsx`. |
| **v1.55** | Sep 2026 | **Asistencia Híbrida Voz/Táctil, Motor Socrático de Integridad Académica, Tokenómica Dual Soroban, Terminal POS Taquilla Web (/pos) y Eduki Guía de Alto Contraste**: Conmutador reactivo de asistencia escolar (`/modules/attendance`) entre dictado por voz continuo (`AttendanceVoiceView.tsx` con Web Speech API, matching difuso NLP Levenshtein y dictado masivo) y grilla táctil manual de 1-toque (`AttendanceManualView.tsx` con botones `[P]`, `[A]`, `[T]`, `[J]`, buscador instantáneo y marcado masivo), preservando la persistencia multi-nivel (`localStorage` + Supabase `attendance_logs` + Smart Contract Soroban de presentismo). Implementación del **Motor Socrático de Integridad Académica** (`/modules/evaluations` & `aiService.ts`) con el robot **Eduki** (`SocraticEvaluationModal.tsx`): adaptación dialéctica por tipología de desafío (Desafíos: 1-2 repreguntas, TPs: 4 fases de Tesis, Antítesis, Síntesis y Aplicación, Exámenes: contrarreloj con cronómetro), diagnóstico en tiempo real de Resiliencia Argumentativa, Profundidad Conceptual y Originalidad Anti-Copia (0-100%), calibración automática de notas (1-10) y recompensas de mérito (1-20 E4C), con **advertencia obligatoria del Tutor Socrático** en asignación de tareas contra copiado de IA e internet. **Eduki Guía Docente** (`AIAssistant.tsx`) con cápsula de alto contraste obsidiana (`#020617`), borde sólido celeste neón de 2.5px (`#38bdf8` / Sky 400), anillo exterior concéntrico (`ring-2 ring-sky-400/50`) y halo ambiental para máxima visibilidad sin FOUC. **Tokenómica Dual Soroban Rust** (`contracts/token_swap` / `E4CCulturalGateway` `#![no_std]`): Quema 1 ($E4C $\rightarrow$ Pase Cultural $ACT) y Quema 2 ($ACT $\rightarrow$ Entrada en Taquilla). **Pase Cultural PWA** (`CulturalPassCard.tsx`) bajo disciplina de tinta única y **Terminal Web POS** (`/pos` / `POSScannerView.tsx`) para comercios y teatros con escaneo por cámara nativa (`BarcodeDetector`), validación de cupón y quema on-chain sin instalación. Optimización de empaquetado Vite (`manualChunks` modulares) con cero advertencias de bundles pesados. |
| **v1.50** | Ago 2026 | **Eduki Profesor Robot Futurista, Conector Cuántico, Sincronización On-Chain, Libro Contable de Doble Partida y Blindaje RBAC Estudiantil**: Rediseño completo de la mascota robot **Eduki** (`EdukiRobotAvatar.tsx`) en silueta 100% libre y transparente, sin recuadros ni marcos de TV: gafas inteligentes holográficas (`eduki-glasses-gleam`), birrete cuántico con borla dorada, traje académico perlado y grafito con insignia estelar, libro digital holográfico interactivo con fórmulas pedagógicas (`eduki-holo-book`), brazo articulado con gesto OK, ciclo de guiño con destello (`✨`) y propulsores de plasma. En `StudentAIWelcomeCard.tsx`, se integró un **conector cuántico holográfico unificado con nodo emisor y haz láser pulsante**. Motor de **sincronización en tiempo real de asistencias y tokens on-chain** con Stellar Horizon Testnet API y Supabase Realtime. Implementación del **Libro Contable de Doble Partida en "Mis Tokens" (`MyTokens.tsx`)**, garantizando la ecuación contable exacta $\mathbf{Balance\ Actual} \equiv \mathbf{Total\ Ganados} - \mathbf{Total\ Canjeados}$. **Blindaje de Seguridad RBAC Estudiantil**: Aislamiento estricto de roles que confina a los alumnos exclusivamente a sus 8 secciones escolares en el Asistente Inicial (`OnboardingTour.tsx`), en el Centro de Ayuda (`HelpModal.tsx` con badge `🎓 Secciones de Alumno`) y en la barra de navegación (`Navigation.tsx`), bloqueando el acceso a herramientas o configuraciones docentes y administrativas. |
| **v1.49** | Ago 2026 | **Formulario Docente Maximizable y Eduki Ultra-Gamificado 3D**: Maximización interactiva del formulario de creación de desafíos (`TaskAssignment.tsx`) en modal flotante de alta resolución con soporte de pantalla completa (`Fullscreen`), atajo `Esc` y auto-minimizado inmediato al pulsar *"Confirmar y Publicar Desafío"*. Auto-apertura maximizada al generar desafíos desde el asistente pedagógico. Gamificación 3D completa de la mascota robot (`EdukiRobotAvatar.tsx`) con animación de guiño de ojo y destello estelar (`✨`), gesto robótico "OK" / pulgar arriba, levitación 3D, ondas cuánticas de antena, viñeta holográfica flotante 3D con perspectiva CSS (`vignette-3d-float`) y unificación oficial del nombre a **Eduki**. |
| **v1.48** | Ago 2026 | **Emisión Automática On-Chain por Smart Contract Soroban**: Automatización integral del flujo de validación y emisión de tokens E4C en Stellar Testnet. Al aprobar un desafío o evaluación pedagógica, el Smart Contract (`EduValidatorContract` / `contractValidator.ts`) ejecuta y transfiere inmediatamente los tokens a la billetera del alumno sin requerir validadores humanos manuales. Sincronizador de emisiones on-chain en 1-clic (`syncPendingTeacherApprovedTasks`) y transferencia directa tras desbloqueo de inconsistencias por parte del Administrador. |
| **v1.47** | Ago 2026 | **Robot Eduki IA Visual, Diagnóstico Holográfico y Gestión de Preceptores**: Mascota robot 3D vector animada (`EdukiRobotAvatar.tsx`) con cuadro de diálogo holográfico (`StudentAIWelcomeCard.tsx`) que detalla desafíos aprobados y pendientes, presentismo y ausencias, evaluación de saldo vs catálogo de marketplace y recordatorio de creación de avatares 3D con tokens, con control de minimizado a cápsula compacta. Tutor IA estudiantil flotante (`StudentAIAssistant.tsx`) con dictado por voz y atajo `/`. Incorporación del **Módulo de Alta y Gestión de Preceptores** (`PreceptorManagement.tsx`) con aislamiento estricto de escuela y cursos autorizados (RBAC). |
| **v1.46** | Ago 2026 | **Módulo Docente de Calificaciones y Evaluaciones** (`TeacherGradesView.tsx`): Matriz académica interactiva de notas y TPs, cálculo de promedio general ponderado (1 a 10), bonificaciones de mérito (+1.5x Tokens), estados académicos (Promocionado, Regular, Recuperatorio), ficha diagnóstica individual y exportación oficial a CSV. |
| **v1.45** | Ago 2026 | **Libro Matriz Mensual de Asistencia y Semáforo CABA** (`MonthlyAttendanceMatrix.tsx`): Planilla mensual de presentismo por escuela, curso y división, cálculo en tiempo real del semáforo reglamentario (Art. 83 bis), badges normativos (P, T, A, J, RA), tokens on-chain auditados y exportación CSV. |
| **v1.44** | Ago 2026 | **Toma de Asistencia con Smart Contracts Soroban e Idempotencia**: Integración con `validate_daily_attendance` (`contractValidator.ts`) y Edge Function `send-e4c-tokens`, validando cuotas diarias (+1 E4C) y previniendo duplicados on-chain. |
| **v1.43** | Ago 2026 | **Arquitectura de Persistencia Total y Keep-Alive (Zero Data Loss)**: Retención en memoria y sincronización con `sessionStorage` en paneles de Estudiantes, Profesores, Administradores, Validadores y Gobierno. Incorporación del **Motor 3D Anti-Sesgo Humano** (`promptEnricher.ts`), **Validación de Smart Contracts Soroban en Aprobación Docente** (`contractValidator.ts`), bandeja de **Revisión de Inconsistencias** (`InconsistencyReview.tsx`) y **Ordenamiento Cronológico Descendente** en el Historial de Desafíos. |
| **v1.42** | Ago 2026 | Integración de Onboarding con Pollar Auth (Embedded Smart Accounts y Trustlines Gasless), Centro de Aprobación Web3 con checkboxes y aprobación masiva en lote, ordenamiento jerárquico multi-criterio, auditoría jurisdiccional de bóvedas y herramienta de purga de docentes. |

---

## 2. Estructura Inicial

### 📑 Tabla de Contenidos
- [1. Portada e Información Documental](#1-portada-e-información-documental)
- [2. Estructura Inicial](#2-estructura-inicial)
  - [Introducción y Propósito](#-introducción-y-propósito)
  - [Requisitos del Sistema](#-requisitos-del-sistema)
- [3. Inicio Rápido y Configuración](#3-inicio-rápido-y-configuración)
  - [Instalación y Acceso](#instalación-y-acceso)
  - [Registro e Inicio de Sesión](#registro-e-inicio-de-sesión)
  - [Activación de Cuenta Digital con Pollar Auth](#-activación-de-cuenta-digital-con-pollar-auth-smart-accounts)
  - [Navegación e Interfaz](#navegación-e-interfaz)
- [4. Guía de Funcionalidades (Cuerpo Principal)](#4-guía-de-funcionalidades-cuerpo-principal)
  - [🎓 4.1. Estudiante (Alumno)](#-41-estudiante-alumno)
    - [Robot Eduki: Mascota 3D Gamificada y Diagnóstico Holográfico](#robot-eduki-mascota-3d-gamificada-diagnóstico-holográfico-y-viñeta-flotante)
    - [Defensa Socrática Anti-Copia en Desafíos con Eduki](#-defensa-socrática-anti-copia-en-desafíos-con-eduki)
    - [Pasaporte Cultural PWA y Canje por Tokens $ACT](#-pasaporte-cultural-pwa-y-canje-por-tokens-act)
    - [Mis Tokens: Libro Contable de Doble Partida y Reconciliación On-Chain](#mis-tokens-libro-contable-de-doble-partida-y-reconciliación-on-chain)
    - [Pasaporte Escolar Digital 3D](#pasaporte-escolar-digital-3d)
  - [👩‍🏫 4.2. Profesor (Docente)](#-42-profesor-docente)
    - [Creación de Desafíos con Eduki y Formulario Maximizable](#creación-de-desafíos-con-eduki-y-formulario-maximizable)
    - [Control Híbrido de Presentismo: Voz Continua y Grilla Táctil](#-control-híbrido-de-presentismo-voz-continua-y-grilla-táctil)
    - [Validación y Aprobación con Smart Contract](#validación-y-aprobación-con-smart-contract)
    - [Módulo de Calificaciones y Evaluaciones Docente](#módulo-de-calificaciones-y-evaluaciones-docente-teachergradesviewtsx)
  - [🤖 4.3. Automatización On-Chain por Smart Contract (EduValidatorContract)](#-43-automatización-on-chain-por-smart-contract-eduvalidatorcontract)
  - [📋 4.4. Preceptoría (Reglamento Escolar CABA — Art. 137)](#-44-preceptoría-reglamento-escolar-caba--art-137)
  - [🏛️ 4.5. Gobierno y Supervisión Escolar](#-45-gobierno-y-supervisión-escolar)
  - [👑 4.6. Administrador de Plataforma](#-46-administrador-de-plataforma)
  - [⚙️ 4.7. Mantenimiento Técnico y DevSecOps](#-47-mantenimiento-técnico-y-devsecops)
  - [🧪 4.8. Guía de Pruebas Rápidas (Sandbox v1.55)](#-48-guía-de-pruebas-rápidas-sandbox-v155)
  - [🎟️ 4.9. Terminal POS Web de Taquilla Cultural (/pos)](#️-49-terminal-pos-web-de-taquilla-cultural-pos)
- [5. Soporte y Solución de Problemas](#5-soporte-y-solución-de-problemas)
  - [Preguntas Frecuentes (FAQ)](#-preguntas-frecuentes-faq)
  - [Matriz de Errores y Soluciones](#-matriz-de-errores-y-soluciones)
  - [Glosario de Términos](#-glosario-de-términos)
  - [Canales de Soporte](#-canales-de-soporte)
  - [Marco Normativo CABA](#🏛️-marco-normativo-cumplimiento-del-reglamento-escolar-de-caba)

---

### 🎯 Introducción y Propósito
**E4C (Education for Culture)** es una plataforma educativa basada en la **Economía del Mérito**. Su propósito fundamental es:
1.  **Transformar el compromiso escolar**: Convertir las actividades pedagógicas tradicionales en **Desafíos** que acreditan reconocimientos escolares en Stellar Testnet.
2.  **Impulsar la permanencia escolar**: Monitorear el presentismo regular y respaldar metas colectivas de curso (Salidas Didácticas y visitas culturales) financiadas directamente por **Empresas Patrocinantes e Instituciones**.
3.  **Garantizar un entorno educativo seguro**: Blindaje absoluto contra la especulación financiera (cero trading o criptomonedas volátiles para menores, Reglamento Escolar CABA Art. 32 [VERIFICAR CON ASESORÍA LEGAL]) y protección estricta de la privacidad de datos (Ley N° 25.326 y Ley N° 26.061).

### 💻 Requisitos del Sistema

*   **Dispositivos Soportados**: Computadoras de escritorio, notebooks, tablets y teléfonos inteligentes con pantalla táctil.
*   **Navegadores Web Recomendados**:
    *   **Google Chrome** (v110+): Recomendado para soporte completo de IA Local (Gemini Nano), Pollar Auth y dictado de voz nativo (`SpeechRecognition`).
    *   **Microsoft Edge** (v110+): Soporte completo para Passkeys locales, Pollar Auth y dictado por voz.
    *   **Apple Safari** (v16+): Soporte para Passkeys WebAuthn, Pollar Auth y visualización 3D.
    *   **Mozilla Firefox** (v115+): Soporte general (el dictado por voz requerirá navegadores basados en Chromium).
*   **Conexión a Internet**: Conexión de banda ancha o red móvil (4G/5G) con soporte HTTPS.

---

## 3. Inicio Rápido y Configuración

### Instalación y Acceso
E4C es una aplicación web responsiva (Web App / PWA). No requiere instalación pesada desde tiendas de aplicaciones:
1.  Accede desde tu navegador a la URL oficial del programa (ej. `https://app.e4c.education`) o a tu entorno local (`http://localhost:5173`).
2.  Si estás en un dispositivo móvil, puedes pulsar en el menú del navegador *"Agregar a la pantalla de inicio"* para utilizarla como aplicación nativa.

### Registro e Inicio de Sesión
1.  **Ingreso con Google (OAuth 2.0)**:
    *   Haz clic en el botón **"Entrar con Google"**.
    *   Selecciona tu cuenta educativa o personal de Gmail.
    *   Si eres nuevo, tu perfil ingresará en estado *"Pendiente"* hasta que la dirección de tu escuela o preceptoría valide tu curso y división.
2.  **Ingreso con Llave de Acceso (Passkey WebAuthn)**:
    *   Si previamente vinculaste tu llave de acceso en este dispositivo, haz clic en **"Entrar con Llave de Acceso (Passkey)"**.
    *   El sistema utiliza la Web Crypto API con derivación segura **PBKDF2 (SHA-512, 100,000 iteraciones)** para desbloquear la sesión de forma instantánea. La autenticación se valida en el hardware local del dispositivo; la plataforma nunca almacena ni transmite datos biométricos [VERIFICAR CON ASESORÍA LEGAL — Ley 25.326, datos sensibles de menores].

---

### 🔐 Activación de Cuenta Digital con Pollar Auth (Smart Accounts)

Para que ningún estudiante ni docente deba lidiar con la complejidad técnica de las criptomonedas, E4C integra **Pollar Auth** como sistema de **Cuenta Digital Educativa Embebida (Smart Account)**:

```text
+-----------------------------------------------------------+
|               Modal de Activación Pollar                  |
|                                                           |
|             [ Icono de Cuenta Digital E4C ]               |
|                                                           |
|             ACTIVA TU CUENTA DIGITAL E4C                  |
|  Para recibir reconocimientos y recompensas escolares,    |
|  necesitas activar tu cuenta digital segura               |
|  (Smart Account) con Pollar. Solo toma un segundo.        |
|                                                           |
|             [ 🔑 Activar Cuenta Digital ]                 |
+-----------------------------------------------------------+
```

#### ¿Cómo Funciona el Flujo de Pollar?
1. **Detección Automática de Cuenta Digital**:
   * Si al iniciar sesión con Google tu perfil no tiene una clave pública de Stellar registrada, la aplicación mostrará automáticamente la tarjeta interactiva de **Pollar Connect**.
2. **Activación con 1-Clic (Sin Frases Semilla)**:
   * Al hacer clic en **"Activar Cuenta Digital"**, se abrirá el modal seguro de Pollar.
   * Elige tu proveedor social (Google, Email o Discord). Pollar generará una cuenta digital no custodial (*Smart Account*) vinculada a tu perfil escolar. **No necesitas anotar frases de 12 o 24 palabras en papel ni instalar extensiones**.
3. **Firma y Activación Gasless (Sin Costo de Transacción)**:
   * Para los estudiantes, Pollar firma de forma patrocinada (*Gasless*) el **Trustline del Token E4C**. No necesitas tener XLM ni pagar comisiones de red para activar tu cuenta.
4. **Sincronización Inmediata**:
   * Tu clave pública se vinculará de inmediato a tu perfil en Supabase y la pantalla se recargará automáticamente lista para recibir recompensas académicas.

---

### Navegación e Interfaz
*   **Splash Screen Cyber-Tech v1.42**: Al iniciar, disfrutarás de una pantalla de carga con telemetría HUD en esquinas (`[ CORE_VERSION: 1.42 ]`), doble anillo giratorio neón y rotación interactiva de tips educativos sobre blockchain Stellar cada 2.5 segundos (con botón de escape *"Omitir"*).
*   **Barra Superior (Header Glassmorphic)**:
    *   Logotipo oficial circular con anillo de neón pulsante.
    *   Identificador del usuario mediante su `@alias` amigable (protegiendo su nombre real en público).
    *   Menú conmutador de roles para administradores y docentes.
*   **Bar Roll y Scroll-to-Top**:
    *   Fina barra neón que mide tu progreso de desplazamiento vertical en tiempo real.
    *   Botón flotante en la esquina inferior derecha para volver al tope de la página con un solo clic.

---

## 4. Guía de Funcionalidades (Cuerpo Principal)

### 🎓 4.1. Estudiante (Alumno)

#### Robot Eduki: Mascota 3D Gamificada, Diagnóstico Holográfico y Viñeta Flotante
Al ingresar a su panel, el estudiante es recibido por **Eduki**, la mascota robot interactiva en 3D vector animado (`EdukiRobotAvatar.tsx` / `StudentAIWelcomeCard.tsx`), con propulsores de levitación, visor digital LED, ondas cuánticas de señal en su antena, **guiño de ojo animado con destello estelar (`✨`)** y **brazo robótico con gesto de aprobación "OK"**:

```text
+---------------------------------------------------------------------------------+
|  [🤖 Robot Eduki 3D]   💬 "¡Buen día, Pablo! 👋" [Viñeta 3D Flotante]           |
|  - Guiño de ojo 😉     -------------------------------------------------------  |
|  - Gesto OK 👌         📝 Tenés 4 trabajos aprobados y 2 pendientes.            |
|  - Levitación 3D 🛸    📅 Registrás 18 presentes y 1 ausente.                   |
|  - Ondas cuánticas 📡  🎟️ ¡Tus 45 E4C ya alcanzan para "Entrada de Cine 2D"!    |
|                        🎨 ¡Recordá que podés usar tokens para crear Avatares!   |
|                        -------------------------------------------------------  |
|                        [🎯 Mis Desafíos]  [🎨 Crear Avatar IA]  [✨ Minimizar]  |
+---------------------------------------------------------------------------------+
```

*   **Gamificación Visual y Reactividad 3D**:
    *   **😉 Guiño de Ojo:** Parpadeo automático y guiño lúdico con destello estelar dorado. Al hacer clic sobre Eduki, saluda y guiña el ojo inmediatamente.
    *   **👌 Gesto "OK" / Pulgar Arriba:** Brazo robótico animado con brazalete neón cian que refuerza positivamente el progreso escolar.
    *   **🛸 Viñeta Flotante 3D (`vignette-3d-float`):** El cuadro de diálogo cuenta con perspectiva tridimensional CSS, sombras de profundidad volumétricas y un haz cuántico que lo conecta físicamente a Eduki.
*   **Diagnóstico Escolar en Tiempo Real**:
    1.  📝 **Desafíos Escolares**: Detalla el balance exacto de tareas aprobadas y pendientes (`"Tenés X trabajos aprobados y Y pendientes"`), señalando entregas en revisión docente.
    2.  📅 **Presentismo y Asistencia**: Monitorea días presentes y ausencias acumuladas en el ciclo lectivo.
    3.  🎟️ **Poder de Canje en el Marketplace**: Evalúa el saldo en tokens E4C contra el catálogo de recompensas de sponsors culturales (*"¡Tus X tokens ya te alcanzan para..."* o *"Te faltan X tokens para..."*).
    4.  🎨 **Recordatorio de Avatares por IA**: Destaca la posibilidad de utilizar tokens E4C para generar personajes 3D exclusivos con IA en la pestaña *"Mi Avatar"*.
*   **Control de Minimizado Inteligente**: El alumno puede presionar **"¡Entendido, minimizar!"** o el botón superior para plegar el cuadro de diálogo en una cápsula compacta flotante (`"🤖 Eduki (2 pendientes)"`), preservando espacio visual y permitiendo reabrir el mensaje completo en cualquier momento con 1 clic.
*   **Tutor Flotante y Arrastrable (`StudentAIAssistant.tsx`)**: Asistente pedagógico flotante movible por la pantalla (soporte touch y mouse), atajo global de teclado (`/`), dictado por voz nativo (`Web Speech API`) y chips de preguntas frecuentes sobre economía escolar y técnicas de estudio.

#### Primeros Pasos y Cuenta Stellar
1.  **Vincular Token E4C**: Si ves un banner amarillo indicando que tu cuenta requiere habilitación, haz clic en **"Vincular Token E4C"** o utiliza el botón de **Pollar Auth** para habilitar el *Trustline* oficial en la red Stellar.
2.  **Tu Alias Público**: El sistema te identifica con un handle único (ej. `@pablosebastian` o `@alias_no_asignado`). Tu nombre real y DNI nunca se exhiben en leaderboards públicos ni en la blockchain.

#### Superación de Desafíos y Desglose de Recompensas
*   **Historial Ordenado por Fecha**: Ingresa a **"Mis Desafíos"** para revisar tus misiones. Todas las tareas se ordenan cronológicamente en orden descendente, garantizando que **el último desafío realizado o actualizado siempre figure arriba**, acompañado por su badge de estado y su fecha/hora exacta de entrega.
*   Al entregar un desafío de tipo **Evaluación**, el sistema calcula y exhibe el desglose en vivo:
    $$\text{Total E4C} = \text{Puntos Base} + \text{Nota del Examen (1 a 10)} + \text{Bono de Excelencia (1.5x)}$$

#### 🛡️ Defensa Socrática Anti-Copia en Desafíos con Eduki
Para garantizar la autenticidad pedagógica, erradicar el copypaste pasivo y entrenar el pensamiento crítico del estudiante, E4C v1.55 incorpora el **Motor Socrático de Integridad Académica** (`SocraticEvaluationModal.tsx` / `aiService.ts`).

Al pulsar **"Entregar Desafío"** en la sección *Mis Desafíos* (`MyTasks.tsx`), no se produce una entrega estática tradicional; se despliega una interfaz dialéctica guiada por el robot **Eduki**:

```text
+---------------------------------------------------------------------------------+
|                       🤖 DEFECTO Y DEFENSA SOCRÁTICA CON EDUKI                 |
|  Desafío: "Análisis del Canto V del Martín Fierro" | Fase 2 de 4: Antítesis     |
|                                                                                 |
|  Eduki: "Sostuviste que Fierro es un personaje puramente victimizado por el     |
|  sistema. ¿Cómo reconciliás esa postura con el duelo a cuchillo con el moreno?" |
|                                                                                 |
|  [ Tu Argumentación Reflexiva...                                            ]  |
|                                                                                 |
|  📊 Radar de Pensamiento en Vivo:                                               |
|  • Resiliencia Argumentativa: 88%  • Profundidad: 82%  • Originalidad: 94%       |
|                                                                                 |
|  [ 🎤 Dictar Argumento ]                                  [ 🚀 Defender Postura ]|
+---------------------------------------------------------------------------------+
```

*   **Fases Dialécticas Adaptativas según la Tipología del Desafío**:
    1.  **Desafíos Cotidianos (1 a 2 repreguntas)**: Cuestionamientos breves de validación conceptual directa para corroborar autoría personal.
    2.  **Trabajos Prácticos (TPs — 4 fases socráticas completas)**:
        *   *Fase 1: Tesis* (Declaración de postura y fundamentación inicial del estudiante).
        *   *Fase 2: Antítesis* (Eduki introduce un contraejemplo, tensión lógica o dilema para probar solidez).
        *   *Fase 3: Síntesis* (Reconciliación lógica e integración conceptual por parte del estudiante).
        *   *Fase 4: Aplicación Práctica* (Transferencia del concepto a un escenario real contemporáneo).
    3.  **Evaluaciones / Exámenes ABP**: Modalidad contrarreloj con cronómetro digital interactivo que desafía al alumno a responder con rapidez y rigor bajo presión temporal.
*   **Métricas del Diagnóstico Dialéctico (Radar 0 a 100%)**:
    *   **Resiliencia Argumentativa**: Mide cómo responde el alumno ante contradicciones y objeciones de Eduki sin abandonar la lógica ni contradecirse.
    *   **Profundidad Conceptual**: Evalúa la densidad de vocabulario técnico, causalidad y referencias al contenido curricular.
    *   **Originalidad Anti-Copia (Motor Heurístico y Redes de LLM)**: Detecta en tiempo real marcas sintéticas de IA (ChatGPT, Claude, Gemini, DeepSeek), viñetas artificiales (`* **Concepto:**`), fórmulas de transición mecánicas (`es importante destacar`, `en conclusión`) o fragmentos de enciclopedias web, premiando la voz genuina del alumno.
*   **Calibración Automática de Notas y Tokens de Mérito**:
    *   Al concluir las rondas dialécticas, Eduki consolida el informe pedagógico, sugiriendo la nota oficial (1 a 10) y calculando la recompensa en tokens E4C (1 a 20 E4C base + bonos de mérito) que luego el docente supervisará con trazabilidad absoluta.
    *   **Penalización Inmediata por Detección de IA**: Si el estudiante copia texto generado por Inteligencia Artificial, la originalidad cae drásticamente (`< 60%`), la nota se reprueba (`<= 4`), se bloquean los tokens (`0 E4C`) y la defensa se califica como **NO APROBADA**.

#### 🔒 Protocolo de Entrega con Doble Validación Obligatoria (Defensa Socrática Aprobada + Evidencia)
Al abrir cualquier desafío en **Mis Desafíos** (`MyTasks.tsx`), la opción de completar la tarea está protegida por un **bloqueo estricto de doble requisito** (`canCompleteTask`):

```text
+---------------------------------------------------------------------------------+
|               CONDICIONES PARA COMPLETAR (2 DE 2 REQUERIDAS)                    |
|                                                                                 |
|   [✓] 1. Defensa Socrática con Eduki: Aprobada (Nota: 9/10 • Originalidad 94%)  |
|   [✓] 2. Enlace de Evidencia: Adjunto y verificado                              |
|                                                                                 |
|          [ 🚀 COMPLETAR Y ENVIAR DESAFÍO ] (Habilitado únicamente si 2/2)       |
+---------------------------------------------------------------------------------+
```

1.  **Requisito 1: Defensa Socrática con Eduki (Validación de Autoría Genuina Aprobada)**:
    *   El estudiante presiona *"Iniciar Defensa Socrática"* y accede de forma **instantánea (0ms)** a la Fase 1 (`getInstantOpeningQuestion`), sin pantallas de carga previas ni demoras de red. Eduki presenta inmediatamente el saludo formativo y la consigna disparadora inicial.
    *   **Detección de Pegado y Copia de IA (0ms)**: El sistema rastrea eventos de pegado directo desde el portapapeles (`onPaste`) y cruza en tiempo real el texto con el catálogo de patrones sintéticos de LLMs (ChatGPT, Claude, Gemini, DeepSeek), viñetas de manual, definiciones enciclopédicas y conectores hiper-formales. Si se detecta copia, el motor genera de forma **inmediata y local (0ms)** la interpelación socrática o el dictamen de no aprobación, sin demoras de red ni retries innecesarios.
    *   **Invalidez por Falta de Originalidad**: Si la defensa final resulta no aprobada por uso de IA (`approved = false`), el estudiante **NO podrá confirmar la defensa** y visualizará un banner de alerta con el botón *"🔄 Reintentar Defensa Socrática (Con tus Propias Palabras)"* para reiniciar la interacción.
2.  **Requisito 2: Adjuntar Enlace de la Evidencia del Trabajo**:
    *   El alumno debe pegar el enlace público a su resolución (Google Drive, GitHub, Canva, Notion, Figma, PDF o enlace web).
3.  **Bloqueo Preventivo del Botón de Envío**:
    *   Si el alumno intenta completar sin haber realizado o sin haber **aprobado** la defensa socrática, el botón permanece **deshabilitado** con el rótulo `🔒 Completar Bloqueado (Faltan Requisitos)`.
    *   Si la defensa socrática fue rechazada por detección de IA, el sistema muestra el badge `❌ No Aprobada (Copia IA)` y la advertencia: *"La defensa socrática fue rechazada por detección de IA o falta de originalidad. Debes reintentarla con tus propias palabras para habilitar la entrega"*.
    *   **Únicamente cuando la defensa está formalmente aprobada y la evidencia adjunta**, el botón se ilumina en gradiente verde-índigo y se habilita para confirmar el envío definitivo al docente.

#### Mi Presentismo & Regularidad (Art. 83 bis CABA)
*   **Historial de Asistencia**: Monitorea tus días presentes, tardanzas (Art. 88.3 CABA) y ausencias justificadas (Art. 90 CABA).
*   **Alerta de Regularidad**: Visualiza el badge de *Alumno Regular* y cuántas faltas te quedan disponibles antes del límite bimestral de 5 inasistencias.
*   **Aporte a la Bóveda**: Cada día de asistencia efectiva suma **+1 E4C** al fondo común de tu curso.

#### Bóvedas Colectivas por División & Desafíos Comunitarios
*   **Meta de Curso (Salidas Didácticas)**: Consulta el fondo acumulado de tu división (ej. *3° "II"*) para financiar visitas culturales guiadas y equipamiento escolar en Stellar.
*   **Desafíos Comunitarios**: Misiones escolares grupales (Eco-Escuela, Maratón de Lectura en Biblioteca Art. 35 CABA) con metas colectivas.

#### Marketplace Cultural & Gestión de Cupones Adquiridos
En E4C v1.61, el **Marketplace Cultural** (`Marketplace.tsx`) incorpora una arquitectura de navegación superior de alta visibilidad que erradica secciones enterradas al fondo de la pantalla y prioriza los beneficios activos:

```text
+---------------------------------------------------------------------------------+
|                       🛍️ MARKETPLACE CULTURAL ESCOLAR                           |
|                                                                                 |
|  [ 🎭 Explorar Catálogo (12) ]          [ 🎟️ Mis Cupones Adquiridos (2 activos) ]|
|  -----------------------------------------------------------------------------  |
|  ⚡ ACCESO RÁPIDO A TUS BENEFICIOS ACTIVOS:                                      |
|  🎟️ Novela Literaria FCE (ACT-1789531993)  •  [ 📱 Ver QR / Pase ]              |
|  -----------------------------------------------------------------------------  |
|  Filtros:  [🟢 Cupones Activos (2)]    [Todos (5)]    [⚪ Ya Utilizados (3)]     |
+---------------------------------------------------------------------------------+
```

1.  **Doble Pestaña Superior Reactiva**:
    *   **`[🎭 Explorar Catálogo ({n})]`**: Catálogo completo de bienes culturales provistos por sponsors (teatro, cine, libros, muestras de arte y gastronomía escolar) con sus costos en tokens E4C (50 a 500 E4C).
    *   **`[🎟️ Mis Cupones Adquiridos ({n} activos)]`**: Vista dedicada y filtrable que exhibe exclusivamente los cupones canjeados por el estudiante, con contador dinámico de cupones activos sin utilizar en tiempo real.
2.  **Tira Superior de Acceso Rápido**:
    *   Si el alumno posee cupones activos sin usar, en la vista del catálogo se despliega automáticamente una barra superior fija con acceso directo en 1 clic: **`[📱 Ver QR / Pase]`**, permitiendo exhibir el pase en taquilla inmediatamente sin realizar scroll ni cambiar de pestaña.
3.  **Priorización Estricta y Filtros por Estado**:
    *   **Activos Primero**: Los cupones disponibles para canjear en boletería o librería se ordenan cronológicamente al inicio con un borde verde esmeralda distintivo (`border-emerald-500/50`).
    *   **Cupones Consumidos**: Los cupones ya validados en taquilla se sitúan debajo con tonalidad atenuada y badge `⚪ Utilizado en Taquilla`.
    *   **Selector de Píldoras**: Filtra al instante entre `[Cupones Activos]`, `[Todos]` y `[Ya Utilizados]`.
4.  **Persistencia Multi-Nivel y Normalización de Vouchers**:
    *   El código único Soroban (`ACT-XXXXXXXXX`) se almacena de forma segura en la base de datos de Supabase en la columna `voucher_uuid` y en la memoria local del navegador (`localStorage`), garantizando disponibilidad inmediata incluso ante fluctuaciones de red.
    *   La Terminal POS Taquilla (`/pos`) reconoce tanto el código alfanumérico como el identificador UUID, previniendo fallos en los puntos de validación de los teatros o librerías.
5.  **Navegación Fluida Sin Recargas Involuntarias (No-Flicker Navigation)**:
    *   Al cerrar la ventana modal de visualización de un código QR pulsando *"Volver al catálogo"*, el sistema preserva la posición y estado de la pantalla sin forzar recargas completas ni disparar animaciones de carga (shimmer) invasivas.
6.  **Interacción Táctil y Generación de Avatares 3D**:
    *   **Acceso Directo desde la Tarjeta Escolar**: El recuadro del avatar en el encabezado del perfil es completamente interactivo.
    *   **Guía para Alumnos Nuevos**: Si el estudiante aún no ha generado un avatar personalizado, el recuadro muestra el mensaje: *"Sin avatar, presioná acá para crearlo"*.
    *   **Auto-Scroll y Foco**: Al hacer clic en el recuadro (tenga o no avatar configurado), la interfaz desplaza la vista suavemente (`scrollIntoView`) hasta centrar el generador de avatares en pantalla y sitúa el cursor de inmediato en el campo de texto del prompt, invitando al estudiante a describir su personaje.

#### 🎟️ Pasaporte Cultural PWA y Canje por Tokens $ACT
En E4C v1.55, el acceso a los bienes culturales de la Ciudad de Buenos Aires (cines, teatros, librerías, museos) se articula mediante una **Tokenómica Dual sobre Smart Contracts Soroban** (`contracts/token_swap` / `tokenSwapService.ts`), separando el token de mérito escolar ($E4C) del token de consumo cultural ($ACT - *Action Cultural Token*).

```text
+---------------------------------------------------------------------------------+
|                       🎟️ PASE CULTURAL DIGITAL ($ACT)                          |
|  Disciplina de Tinta Única: Papel (#F4F1EA) & Teja Cultura (#A6402B)             |
|                                                                                 |
|  TEATRO SAN MARTÍN — SALA CASACUBERTA                                           |
|  Beneficiario: @pablosebastian  •  División: 4° 2da                              |
|  Código Oficial: ACT-8F2K91     •  Fecha: 24 Sep 2026                           |
|                                                                                 |
|          [ ⬛⬛⬛⬛⬛⬛⬛ ]   CÓDIGO QR SEGURO                                  |
|          [ ⬛  QR  ⬛ ]   Para presentar en la taquilla del teatro          |
|          [ ⬛⬛⬛⬛⬛⬛⬛ ]   o comercio cultural adherido                      |
|                                                                                 |
|  Estado: [🟢 DISPONIBLE / VERIFICADO]                                           |
|  Smart Contract Soroban: E4CCulturalGateway::swap_e4c_for_act                   |
+---------------------------------------------------------------------------------+
```

*   **Doble Quema On-Chain (Mecanismo No-Especulativo)**:
    1.  **Quema 1 ($E4C $\rightarrow$ $ACT)**: En el Marketplace, el alumno canjea sus tokens E4C acumulados por mérito escolar. El Smart Contract quema los $E4C y acuña un Pase Cultural $ACT intransferible con su respectiva credencial y código alfanumérico único (`ACT-XXXXXX`).
    2.  **Quema 2 ($ACT $\rightarrow$ Entrada Física)**: Al presentarse en el teatro, cine o librería, el encargado de taquilla escanea el QR o tipea el código en la **Terminal Web POS (`/pos`)**, ejecutando la quema definitiva del token $ACT on-chain (`burn_act_for_ticket`) y entregando la entrada o libro en mano.
*   **Tarjeta de Billete Cultural (`CulturalPassCard.tsx`)**:
    *   Diseñada bajo la estética de **tinta única y papel editorial** (Teja Cultura `#A6402B`, Papel `#F4F1EA`, Verde Verificado `#2F6B58`, Azul Acta `#1B3A5C`), eliminando elementos superfluos y facilitando la legibilidad en pantallas de bajo brillo o impresiones físicas.
    *   Genera un código QR de alta resolución con el payload criptográfico del pase y badge de verificación en tiempo real.
*   **Generador 3D con IA (Personajes, Mascotas y Objetos)**:
    *   Escribe lo que deseas crear: un personaje fantástico, una mascota compañera o un objeto/artefacto legendario.
    *   **Identidad y Género 3D Inteligente**:
        *   *Inferencia Automática y Privada*: El sistema detecta el género del estudiante a partir de su nombre de pila en su perfil (ej. *Pablo* $\rightarrow$ Masculino, *Sofía* $\rightarrow$ Femenino) sin enviar nunca su nombre a la IA (cumpliendo Ley N° 25.326 y Ley N° 26.061).
        *   *Selector de Estilo*: El alumno puede alternar manualmente entre **`👦 Masculino`**, **`👧 Femenino`** o **`✨ Neutro`**.
        *   *Prioridad del Prompt*: Si el alumno solicita explícitamente un género (ej: *"una maga astronauta"*, *"un perrito macho"*) o explícitamente solicita **sin género / neutro / andrógino** (ej: *"un robot sin género"*, *"un alienígena neutro"*), el prompt toma prioridad absoluta.
    *   Costo dinámico: *Simple (2 E4C)*, *Medio (4 E4C)*, *Avanzado (6 E4C)*.
    *   Los avatares se guardan en tu galería para intercambiarlos gratis en cualquier momento.
    *   **Papelera de Reciclaje de 30 Días**: Permite enviar avatares a la papelera, restaurarlos o purgarlos definitivamente, con auto-limpieza periódica.

##### 🛡️ Restricciones y Limitaciones de Seguridad para Alumnos Menores (Ley N° 25.326 / Ley N° 26.061 / Art. 32 Reglamento Escolar CABA [VERIFICAR CON ASESORÍA LEGAL])
Para resguardar la seguridad física, psicológica y digital de los estudiantes, el generador de imágenes cuenta con un **motor de moderación estricto en doble capa** (validación inmediata en frontend y filtrado criptográfico en la Edge Function):

1.  **🚫 Prohibición de Datos Personales (PII)**:
    *   No se permite ingresar correos electrónicos, números de DNI, teléfonos, direcciones físicas ni nombres reales completos en los prompts.
2.  **🎭 Estilización 3D Obligatoria (Prevención de Deepfakes)**:
    *   Todas las creaciones se renderizan forzosamente en formato **3D digital estilizado (estética animación 3D Pixar / Disney / Escultura Digital)**. Esto previene la generación o alteración de fotografías realistas de menores de edad y combate el ciberacoso escolar.
3.  **⛔ Tolerancia Cero a Contenido Adulto / Inapropiado (NSFW)**:
    *   Bloqueo de términos sexuales, desnudez, vestimenta inapropiada o poses sugerentes.
4.  **⚔️ Prohibición de Violencia, Armas y Sangre**:
    *   Bloqueo de armas de fuego reales, armas blancas, heridas, sangre, mutilaciones, terrorismo o incitación al daño propio o ajeno.
5.  **🚭 Prohibición de Drogas, Alcohol y Sustancias**:
    *   Filtro contra cualquier mención de bebidas alcohólicas, cigarrillos, tabaco, vapeo y sustancias ilegales.
6.  **🎲 Cumplimiento Anti-Ludopatía y Especulación (Reglamento Escolar CABA Art. 32 [VERIFICAR CON ASESORÍA LEGAL])**:
    *   Prohibición absoluta de elementos asociados a casinos, mesas de ruleta, cartas de póker, apuestas deportivas, máquinas tragamonedas o interfaces de trading bursátil.
7.  **🤝 Convivencia y Prevención de Bullying**:
    *   Filtro estricto contra discursos de odio, simbología discriminatoria, insultos o ataques hacia otros estudiantes.
8.  **✨ Enfoque en Creatividad Sana y Coherencia de Identidad**:
    *   Los alumnos pueden solicitar libremente **Mascotas 3D** (perros superhéroes, gatitos astronautas, dragones), **Objetos 3D** (naves espaciales, libros mágicos, robots, cristales) y **Personajes 3D** (científicas, astronautas, magos, deportistas), respetando pedidos explícitos de género femenino, masculino o neutralidad/sin género.

#### Mis Tokens: Libro Contable de Doble Partida y Reconciliación On-Chain
En la pestaña **"Mis Tokens"** (`MyTokens.tsx`), el estudiante dispone de un libro mayor contable transparente y auditable que garantiza paridad matemática absoluta:

$$\mathbf{Balance\ Actual\ E4C} \equiv \mathbf{Total\ Ganados} - \mathbf{Total\ Canjeados}$$

*   **Total Ganados (Créditos 📥):**
    *   **Desafíos Aprobados (`student_tasks`):** Puntos base de la consigna + Nota académica del examen (1 a 10) + Bonificación de mérito (+1.5x).
    *   **Presentismo Escolar (`attendance_logs`):** +1 E4C por cada jornada presente o tardanza registrada por el docente o preceptor.
    *   **Acreditaciones On-Chain Stellar:** Pagos directos recibidos en la clave pública del alumno en Stellar Horizon Testnet.
*   **Total Canjeados (Débitos 📤):**
    *   **Canjes del Marketplace (`redeems`):** Vouchers de cine, teatro, libros o refrigerios con costos oficiales de catálogo (50 a 500 E4C).
    *   **Diseño de Avatares 3D con IA (`avatar_config.library`):** Tokens consumidos según la complejidad del prompt (2, 4 o 6 E4C).
    *   **Transferencias On-Chain Stellar:** Pagos salientes o quemas de tokens oficiales.
*   **Trazabilidad y Sincronización en Tiempo Real:**
    *   Cada movimiento dispone de su badge contextual (**Desafío 📝**, **Asistencia 📅**, **Marketplace 🎟️**, **Avatar IA 🎨**, **Blockchain ⛓️**), fecha y hora exacta, y código de referencia único.
    *   El balance se sincroniza automáticamente con `profiles.tokens` y la red Stellar, actualizándose al instante mediante canales **Supabase Realtime**.

#### Pasaporte Escolar Digital 3D
*   **Giro 3D**: Haz doble clic para girar la credencial y examinar tus visas de materias aprobadas con promedios reales (ej. `Matemáticas 8.50`).
*   **Botón "Ver Detalles"**: Despliega tu panel glassmorphic con 4 KPIs escolares (Desafíos Aprobados, Promedio General, Mérito Total y Sponsor Favorito).
*   **Zoom Pantalla Completa**: Toca la credencial para maximizarla en un Lightbox de alta resolución.

##### 🛡️ Aislamiento Estricto de Roles (RBAC), Asistente Inicial y Centro de Ayuda
En estricto apego al *Reglamento Escolar de Educación Obligatoria de CABA* [VERIFICAR CON ASESORÍA LEGAL] y a normativas de protección de menores (Ley N° 25.326 y Ley N° 26.061), el sistema garantiza un **aislamiento absoluto del perfil del estudiante**:
1.  **Navegación Restringida (`Navigation.tsx`)**: La barra superior confina al alumno a alternar únicamente entre su panel **"Estudiante"** y el **"Ranking"** escolar. Quedan automáticamente ocultas e inaccesibles las pestañas de roles privilegiados (*Docente*, *Preceptor*, *Admin* y *Gobierno*).
2.  **Asistente Inicial y Centro de Tutoriales (`OnboardingTour.tsx`)**: Al ingresar por primera vez o reabrir el tour, el menú desplegable lista de forma exclusiva las **8 secciones de estudiante**:
    *   🎯 *Mis Desafíos*: Entrega de consignas y cobro de tokens.
    *   📅 *Mi Presentismo*: Asistencia diaria, cómputo de tardanzas y semáforo CABA (Art. 83 bis [VERIFICAR CON ASESORÍA LEGAL]).
    *   👥 *Bóveda Colectiva*: Fondos compartidos para salidas didácticas de división.
    *   💰 *Mis Tokens*: Auditoría de saldo en la red Stellar Testnet y libro mayor de doble partida.
    *   🏆 *Mis Logros NFT*: Diplomas y distinciones académicas acuñadas on-chain.
    *   🛍️ *Marketplace Cultural*: Canje de vouchers de cine, teatro y librerías.
    *   ✨ *Mi Avatar 3D con IA*: Generador de personajes estilizados con DALL-E / Pollinations.
    *   💳 *Credencial Digital*: Pasaporte 3D con visas de materias y promedios.
3.  **Centro de Ayuda y Documentación (`HelpModal.tsx`)**:
    *   El centro de ayuda detecta el rol verificado del estudiante en el contexto de autenticación.
    *   Muestra el identificador oficial **`🎓 Secciones de Alumno`** y oculta los selectores de otros roles.
    *   El motor de búsqueda y la lista de preguntas frecuentes filtra exclusivamente las 10 consultas pertinentes para el estudiante, bloqueando el acceso a configuraciones docentes (reversión de notas masivas, cuotas de smart contracts o administración de infraestructura Stellar).

---

### 👩‍🏫 4.2. Profesor (Docente)

#### Asistente Pedagógico Eduki Guía, Borde de Alto Contraste y Formulario Maximizable
Para potenciar la planificación de consignas sin sobrecargar al educador, el asistente docente **Eduki Guía** (`AIAssistant.tsx`) y el formulario de asignación (`TaskAssignment.tsx`) cuentan con un flujo de trabajo optimizado:
1.  **Borde Sólido Celeste Neón y Relieve Visual en Eduki Guía**:
    *   La cápsula flotante incorpora un **borde sólido de 2.5px celeste neón (`#38bdf8`)**, un anillo exterior concéntrico (`ring-2 ring-sky-400/50`) y halo luminoso ambiental (`boxShadow`).
    *   Esto garantiza un **contraste visual inmediato** y evita que el botón se mimetice con fondos pasteles o sufra parpadeos visuales (FOUC).
2.  **Advertencia Obligatoria del Tutor Socrático Anti-Copia IA**:
    *   Toda consigna creada manual o asistidamente incorpora en sus instrucciones la notificación legal y pedagógica:  
        *«No se aceptará copiado y pegado de respuestas generadas por Inteligencia Artificial ni textos de internet. La entrega será evaluada socráticamente requiriendo fundamentación con tus propias palabras.»*
3.  **Generación y Relleno Asistido de Desafíos**:
    *   Al solicitar *"Genera este desafío escolar"*, Eduki Guía no solo redacta la consigna y calibra las recompensas, sino que **navega automáticamente a la pestaña 'Asignar Desafíos' y abre el formulario maximizado** con todos los campos precompletados (materia, curso, división, tipo de desafío, tokens y consigna).
    *   **Auto-Minimizado Focal**: Tras inyectar con éxito los datos generados en el formulario principal, Eduki Guía se minimiza automáticamente a su cápsula flotante, despejando la pantalla para que el docente pueda enfocar el 100% de su atención en la revisión, ajuste y publicación de la consigna.
4.  **Formulario de Desafío Maximizable a Pantalla Completa (`TaskAssignment.tsx`)**:
    *   **Botón de Maximizar**: En la cabecera del formulario de asignación, el botón de maximizar expande el formulario a un **modal flotante de alta resolución** (o modo *Fullscreen*).
    *   **Edición Cómoda**: Permite redactar rúbricas extensas, verificar los badges de recompensa (1 a 20 E4C) y ajustar los destinatarios con total claridad visual.
    *   **Auto-Minimizado al Publicar**: Al presionar **"Confirmar y Publicar Desafío"**, el sistema crea y difunde la actividad escolar y **minimiza automáticamente el formulario**, devolviendo al docente a la vista general limpia.
    *   **Atajo de Cierre**: Presiona la tecla <kbd>Esc</kbd> o el botón de minimizar para regresar a la vista compacta sin perder cambios.
5.  **Reconocimientos Calibrados**:
    *   *Cotidianos*: 1 a 5 E4C.
    *   *Trabajos Prácticos (TPs)*: 6 a 12 E4C.
    *   *Evaluaciones / ABP*: 13 a 20 E4C.

#### 📖 Guías Pedagógicas Low-Touch Instantáneas y Motor de Orientación Formativa (`pedagogical_guidance`)
El asistente docente **Eduki Guía** (`AIAssistant.tsx`) incorpora en su pie de consulta tres píldoras de conocimiento institucional directo que responden con **cero latencia** de red y plena disponibilidad offline:

1. **📖 Guía Régimen Académico CABA (Res. N° 223/MEDGC/26):**
   * **Principio de Avance Continuo:** La evaluación se concibe como una herramienta de retroalimentación formativa en proceso, erradicando el promedio aritmético ciego que penaliza el error inicial en pos de la trayectoria real demostrada por el estudiante.
   * **3 Niveles de Logro Ministeriales:**
     * **Inicial:** Comprensión incipiente; requiere andamiaje docente y reformulación guiada.
     * **En Proceso:** Comprensión funcional con vacíos conceptuales o dificultad de extrapolación a escenarios inéditos.
     * **Logrado:** Dominio reflexivo, fundamentación autónoma y resolución contextualizada con lenguaje técnico formal.
   * **Integración con Notas & Evaluaciones:** En la pestaña *Notas & Evaluaciones*, cada entrega calificada con Eduki calibra estos 3 niveles en tiempo real con sus recompensas asociadas (1 a 20 E4C).

2. **💡 Dinámicas Socráticas de Debate en Aula:**
   * **Pecera Dialéctica (Fishbowl):** 4 sillas en el centro discuten una tesis provocadora con 1 silla vacía rotatoria que permite a cualquier estudiante del círculo exterior intervenir con un contraejemplo o refutación y luego regresar a su asiento.
   * **Equipos de Perspectivas Contrapuestas (Abogado del Diablo):** División del curso en Postura A, Postura B y Panel Validador/Auditor, defendiendo argumentos asignados al azar para desarrollar empatía cognitiva y resiliencia argumentativa.
   * **Ronda Relámpago de Preguntas Provocadoras (1 min sin juzgar):** Lluvia espontánea de hipótesis previas a la formalización teórica a partir del disparador inicial del kit curricular.

3. **🛡️ Integridad Académica y Detección Formativa Anti-Copia de IA:**
   * **Identificación de Texto Sintético:** Detección de prosa enciclopédica despersonalizada, desconectada de la vivencia del aula y con vocabulario avanzado que el estudiante no puede explicar coloquialmente.
   * **Intervención Socrática no Punitiva:** Sin acusaciones directas ("esto lo hiciste con ChatGPT"), se repregunta sobre el significado de los términos clave y se solicita un contraejemplo de aplicación cotidiana.
   * **Devolución Constructiva:** Invitación a dialogar con el Tutor Eduki para validar el razonamiento genuino y acreditar el mérito escolar.

4. **Desacoplamiento de la Edge Function (`generate-ai-evaluation` & `aiService.ts`):**
   * La infraestructura de IA admite formalmente la acción `pedagogical_guidance`, permitiendo a los docentes realizar cualquier pregunta didáctica, metodológica o conceptual en lenguaje natural desde el campo de texto de Eduki Guía sin sufrir errores de esquema HTTP 400 (`unknown_action`) ni bloqueos en la interfaz.

#### 📈 Motor de Continuidad Pedagógica y Avance Continuo (Res. N° 223/MEDGC/26)
Para asegurar que los desafíos no sean actividades aisladas sino una trayectoria formativa coherente, **Eduki Guía** (`AIAssistant.tsx`) integra un motor de análisis reactivo alineado con el principio de *Avance Continuo* de la Secundaria Aprende de CABA:

1. **Detección Dinámica del Desafío Anterior:**
   * Al abrir Eduki Guía o cambiar de materia/curso, el sistema audita en tiempo real las tareas publicadas (`tasks`).
   * Si existe un desafío previo, la tarjeta superior de **Continuidad Pedagógica** visualiza su título, tipología (*Desafío*, *TP*, *Evaluación*) y puntaje E4C otorgado.
   * El mensaje de bienvenida se adapta automáticamente informando: *"Detecté que tu último desafío fue '[Título]' ([Puntos] E4C). Puedo ayudarte a articular el siguiente desafío aumentando progresivamente la dificultad o diagnosticar la trayectoria del curso"*.

2. **Escalabilidad de la Zona de Desarrollo Próximo (ZDP):**
   * **De Desafío (1 a 10 E4C) $\rightarrow$ Trabajo Práctico (TP, 10 a 14 E4C):** De la comprensión conceptual básica e hipótesis espontáneas hacia el análisis crítico, relación de variables y fundamentación con fuentes.
   * **De TP (10 a 14 E4C) $\rightarrow$ Evaluación Integral / ABP (15 a 20 E4C):** Hacia la resolución de dilemas situados, confrontación dialéctica y síntesis argumentativa autónoma.
   * **De Evaluación (15 a 20 E4C) $\rightarrow$ Proyecto de Transferencia (20 E4C):** Aplicación a problemas reales del entorno escolar o barrial de CABA y producción pública.

3. **Acciones Tácticas en 1 Clic:**
   * **📈 Generar Siguiente en Dificultad:** Envía a la IA el contexto completo del desafío previo (`<desafio_anterior>`), redactando la consigna sucesiva que retoma los conceptos anteriores, eleva el nivel cognitivo, calibra los E4C, incluye la cláusula socrática obligatoria y **abre el formulario en modo maximizado** listo para confirmar.
   * **📊 Analizar Trayectoria:** Brinda al docente un diagnóstico formativo inmediato sobre la competencia base adquirida, el siguiente salto cognitivo recomendado y las estrategias de andamiaje socrático.
   * **🚀 Iniciar Secuencia (Nivel 1):** Si el curso aún no registra tareas en el sistema, guía al docente para lanzar un desafío fundacional diagnóstico con disparador reflexivo.

#### 🗂️ Guía de Bolsillo Low-Touch y Micro-Learning Docente (`TeacherPocketGuide.tsx`)
Para facilitar la adopción inmediata de la plataforma en el aula y reducir a cero la fricción operativa durante la clase, los docentes cuentan con la **Guía de Bolsillo Low-Touch**:

1.  **Tarjeta de Aula Imprimible**:
    *   Ficha sintética y laminada diseñada para tener junto al libro de temas o escritorio docente.
    *   Centraliza el glosario estandarizado de comandos de voz para la toma de asistencia por NLP: `"Presentes todos"`, `"Ausentes: [Apellido]"`, `"Tarde: [Apellido]"`, `"Justificado: [Apellido]"`.
2.  **Módulo de Micro-Learning (< 60s)**:
    *   Carrusel de cápsulas formativas ultra-breves enfocadas en dinámicas concretas de aula (toma de asistencia por voz, corrección socrática, calibración de notas y canje cultural).
    *   **Bloqueo Preventivo y Estado "Próximamente"**: Los videos en etapa de rodaje o preproducción cuentan con un contenedor visual oscurecido, cursor deshabilitado (`cursor-not-allowed`), badge distintivo **"Próximamente"** y tooltip explicativo informando que el material audiovisual estará disponible en la próxima actualización, evitando clics confusos o pantallas de error al educador.
3.  **Mesa de Ayuda Directa por WhatsApp**:
    *   Acceso en 1 toque al canal institucional de soporte ágil vía WhatsApp (`+54 9 11 2634-8727`), resolviendo consultas pedagógicas o incidencias técnicas directamente desde el celular del docente.

#### 📋 Control Híbrido de Presentismo: Voz Continua y Grilla Táctil (`/modules/attendance`)
En E4C v1.55, el registro de asistencia para Docentes y Preceptores incorpora un selector conmutador reactivo de alto rendimiento que permite alternar instantáneamente entre dos modos de trabajo ergonómicos, manteniendo intacta la persistencia multi-nivel:

```text
+---------------------------------------------------------------------------------+
|               SISTEMA DE ASISTENCIA ESCOLAR HÍBRIDA (v1.55)                     |
|  Escuela: Colegio N° 1 D.E. 3  •  Curso: 4° 2da  •  Fecha: 24/09/2026           |
|                                                                                 |
|  MODALIDAD:  [ 🎙️ Toma por Voz Continua ]   [ 🖱️ Grilla Táctil Rápida ]        |
+---------------------------------------------------------------------------------+
```

1.  **Modo Voz Continua (`AttendanceVoiceView.tsx`)**:
    *   **Dictado Fluido con Reconocimiento Nativo**: Utiliza la Web Speech API en español con escucha continua. El docente o preceptor puede presionar *"Iniciar Escucha Continua"* y nombrar estudiantes y estados con naturalidad (ej: *"Gómez presente, Pérez ausente, Rodríguez tarde, Fernández presente"*).
    *   **Matching Inteligente con NLP Difuso (Distancia Levenshtein)**: El motor compara fonética y ortográficamente las palabras capturadas contra la nómina oficial del curso, tolerando ruido ambiente, apodos o pronunciaciones imperfectas con umbral de similitud configurable.
    *   **Dictado Masivo en Bloque**: Dispone de un área de procesamiento rápido para dictar nóminas enteras en una sola frase (*"Todos presentes excepto Benítez y Morales"*), detectando excepciones automáticamente.
2.  **Modo Grilla Táctil Rápida (`AttendanceManualView.tsx`)**:
    *   **Botones 1-Toque**: Botones táctiles de gran tamaño para cada alumno: `[P]` (Presente en verde), `[A]` (Ausente en rojo), `[T]` (Tardanza en amarillo), `[J]` (Justificada en azul).
    *   **Buscador Instantáneo**: Campo de filtrado en vivo por nombre, apellido o `@alias`.
    *   **Acciones Masivas en 1-Clic**: Botones directos *"Todos Presentes"* y *"Marcar Resto como Ausentes"*.
3.  **Persistencia Multi-Nivel y Blindaje de Datos**:
    *   **Nivel 1 (Inmediato)**: Volcado instantáneo en `localStorage` (`e4c_attendance_logs_${studentId}`). Cero pérdida de datos ante desconexiones.
    *   **Nivel 2 (Nube)**: Sincronización asíncrona con Supabase (`attendance_logs`) sanitizando columnas reales y UUID de autoridad.
    *   **Nivel 3 (On-Chain)**: Registro de presentismo en el Smart Contract Soroban (`validate_daily_attendance`), acreditando +1 E4C por jornada efectiva y previniendo colisiones de doble presente.

#### Validación y Aprobación con Smart Contract
*   Al revisar un desafío, el docente ingresa la calificación o bonos de mérito y pulsa **"Aprobar con Smart Contract"**.
*   **Verificación y Emisión On-Chain Inmediata**: El motor [`contractValidator.ts`](file:///C:/E4C-Desarrollo/src/lib/contractValidator.ts) valida las 6 reglas de `EduValidatorContract` y ejecuta la transacción directamente en Stellar:
    1. *Estado Docente Activo*.
    2. *Monto de Recompensa dentro de límites (1 a 40 E4C)*.
    3. *Prevención de Acreditación Duplicada*.
    4. *Cuota Diaria del Docente ($\le 1000$ E4C/día)*.
    5. *Límite de Colusión Alumno-Docente ($\le 100$ E4C/día)*.
    6. *Cuenta Stellar & Trustline en Alumno*.
*   **Modal de Telemetría On-Chain**:
    *   **Si es Aprobado**: El Smart Contract invoca la Edge Function `send-e4c-tokens`, transfiriendo los tokens inmediatamente desde la cuenta distribuidora institucional (`distributor`) a la billetera Stellar del alumno. Despliega confirmación con hash de Stellar y actualiza el estado directamente a `validator_approved` ("Validado & Acreditado en Blockchain").
    *   **Si detecta Inconsistencias**: Explica la anomalía y deriva automáticamente el desafío a **Revisión del Administrador** (`admin_review`).
*   **Botón de Sincronización Manual (`syncPendingTeacherApprovedTasks`)**: Permite forzar en 1-clic la emisión en Stellar de cualquier entrega que haya quedado en cola.

#### Módulo de Calificaciones y Evaluaciones Docente (`TeacherGradesView.tsx`)
*   **Matriz Académica Interoperable**: Cruza en tiempo real la nómina de alumnos con todos los Trabajos Prácticos y Desafíos del curso y materia.
*   **Cálculo Automático de Promedio Ponderado**: Calcula el promedio general en escala 1 a 10 con badges de desempeño (Distinguido 8-10, Aprobado 6-7, Desaprobado 1-5).
*   **Acreditación de Bonificaciones de Mérito**: Resalta bonos (+1.5x Tokens) y estados académicos reglamentarios (*Promocionado*, *Regular*, *Recuperatorio*).
*   **Ficha Académica Individual & Exportación CSV**: Modal con evidencias de entrega, feedback pedagógico y diagnóstico de IA, junto con exportación oficial a planilla `.csv`.

#### Framework de Gobernanza en IA para Docentes
*   **🔄 Rollbacks (Deshacer en 1-Clic)**: Revierte cualquier sugerencia o borrador generado por la IA antes de publicarlo o grabarlo en la base de datos.
*   **🔍 Traces (Huella de Razonamiento)**: Audita la justificación pedagógica, consignas y evidencias detectadas por la IA en cada corrección (cero cajas negras).
*   **🎯 Intelligent Approvals (Human-in-the-Loop)**: La acreditación oficial de calificaciones y transferencias en Stellar se ejecuta de forma segura con confirmación expresa del docente.

---

### 🤖 4.3. Automatización On-Chain por Smart Contract (`EduValidatorContract`)

En la red Stellar, el contrato inteligente **`edu_validator`** (Soroban) audita y emite las transacciones de forma 100% autónoma, prescindiendo de un perfil validador humano manual:
*   **Emisión Instantánea**: Al recibir la aprobación docente, valida los límites criptográficos y ejecuta el pago on-chain hacia la wallet del alumno.
*   **Cupo Diario por Docente**: Límite de **1000 E4C diarios** de emisión por profesor para evitar inflación no autorizada.
*   **Límite Anticolusión**: Máximo de **100 E4C diarios por par (Docente, Alumno)** para mitigar favoritismos.
*   **Prevención de Doble Gasto**: Verificación criptográfica on-chain (`DataKey::StudentChallenge`) para impedir que un alumno valide dos veces el mismo desafío.
*   **Unicidad On-Chain de Asistencia Diaria (`validate_daily_attendance`)**: Validación criptográfica mediante la clave `DataKey::StudentAttendance(student, subject_id, day_epoch)` para asegurar que ningún estudiante pueda recibir más de 1 presente (+1 E4C) por materia por día.
*   **Resolución de Inconsistencias**: Las transacciones que excedan límites no fallan de forma opaca; generan alertas auditables en `InconsistencyReview.tsx` donde el Administrador puede realizar un override con emisión on-chain automática.

---

### 📋 4.4. Preceptoría (Reglamento Escolar CABA — Art. 137)

El panel de Preceptoría (`PreceptorDashboard.tsx`) centraliza la gestión del régimen de asistencia bajo un **modelo estricto de aislamiento por roles (RBAC)**:
1.  **Aislamiento Estricto de Escuela y Cursos Autorizados**:
    *   El preceptor solo visualiza su **escuela asignada** (bloqueada sin opción de cambio) y únicamente los **cursos específicos** asignados por el administrador (ej: *1ro* y *2do*).
    *   No puede acceder ni modificar datos de cursos o escuelas ajenas a su designación institucional.
2.  **Modalidades de Toma Diaria (`DailyAttendanceModule.tsx`)**:
    *   *Manual en 1-Clic*: Botones oficiales `P` (Presente), `A` (Ausente), `T` (Tardío — Art. 88.3), `RA` (Retiro Anticipado — Art. 88.4), `J` (Justificado — Art. 90).
    *   *Dictado por Voz*: Dicta los ausentes y tardanzas en voz alta para procesamiento inteligente automático con Eduki.
3.  **Libro Matriz Mensual de Asistencia (`MonthlyAttendanceMatrix.tsx`)**:
    *   Auditoría de planilla mensual día por día, con navegación entre meses y cálculo dinámico del **Semáforo de Regularidad CABA** (🟢 Regular $\ge 85\%$, 🟡 En Advertencia $75-84\%$, 🔴 Riesgo Crítico $<75\%$ o $\ge 10$ inasistencias).
    *   Conteo de tokens E4C acreditados on-chain y exportación oficial a `.csv`.
4.  **Acreditación Automática e Idempotente**: Cada presente o tardío acredita **+1 E4C** en la cuenta personal del estudiante y en la Bóveda de División. El sistema previene duplicados mediante verificación de partes previos.

---

### 🏛️ 4.5. Gobierno y Supervisión Escolar

*   **Panel Jurisdiccional (`CollectiveVaultsAudit.tsx`)**: Monitoreo en tiempo real de todas las divisiones escolares de CABA con cálculo dinámico de `student_tasks` y `attendance_logs`.
*   **Telemetría de Trayectorias**: Visualización de tasas de presentismo regular (Art. 83 bis CABA), entregas a tiempo y promedios reales por escuela.
*   **Filtros Avanzados y Suscripción Realtime**: Filtro por institución escolar y estado de bóveda (*En Progreso* / *Desbloqueadas*), con botón de refresco manual.
*   **Exportación Oficial CSV**: Descarga de reportes integrales con fecha (`auditoria_bovedas_colectivas_caba_YYYY-MM-DD.csv`) estructurados con todos los campos auditables de la jurisdicción.

---

### 👑 4.6. Administrador de Plataforma

*   **Módulo de Alta y Gestión de Preceptores (`PreceptorManagement.tsx`)**:
    *   *Pestaña "Preceptores"*: Formulario para dar de alta preceptores con nombre, email institucional, escuela asignada, cursos autorizados (multi-select) y divisiones a cargo.
    *   *Nómina en Vivo y Reasignación*: Visualización de badges con cursos habilitados, modal de edición rápida en 1 clic y baja de perfiles.
    *   *Generador de QR de Registro*: Generación de enlaces y códigos QR específicos para el rol de preceptor (`RegistrationQR.tsx`).
*   **Centro de Aprobación Web3 con Checkboxes y Acciones en Lote**:
    *   *Casillas Individuales*: Checkbox a la izquierda de cada solicitud para selección selectiva.
    *   *Control Maestro*: Botón **"Seleccionar Todos"** / **"Deseleccionar Todos"** con contador en tiempo real (`X de N marcados`).
    *   *Aprobación Masiva*: Botón **"Aprobar Seleccionados (N)"** con barra de progreso animada que procesa la aprobación en Supabase, la activación de cuentas Stellar (`trigger-wallet-creation`) y la vinculación de tokens (`link-e4c-token`) de forma secuencial y transparente.
    *   *Rechazo Masivo*: Botón **"Rechazar (N)"** para descartar solicitudes inválidas en bloque.
*   **Ordenamiento Jerárquico de Usuarios**: Las solicitudes y nóminas de alumnos se ordenan automáticamente por:
    $$1. \text{Escuela (A-Z)} \longrightarrow 2. \text{Curso (1° a 6°)} \longrightarrow 3. \text{División} \longrightarrow 4. \text{Nombre Alfabético}$$
*   **Gestión de Docentes y Herramienta de Purga**: Eliminación segura de tareas, entregas y partes asociados a un docente específico.
*   **Revisión y Desbloqueo de Inconsistencias del Smart Contract (`InconsistencyReview.tsx`)**:
    *   *Pestaña "Inconsistencias"*: Badge numérico con el total de desafíos observados por el contrato inteligente en tiempo real.
    *   *Diagnóstico On-Chain Transparente*: Exposición de la regla vulnerada (`TeacherDailyLimitExceeded`, `StudentTeacherLimitExceeded`, `ChallengeAlreadyCompleted`, `InvalidRewardAmount`, etc.), estudiante, docente, evidencia y cálculo de tokens.
    *   *Aprobar y Desbloquear (Override Administrativo)*: Permite al administrador ingresar una justificación de auditoría, aprobando la excepción y remitiendo la transacción al Validador Técnico para el pago final en Stellar.
    *   *Rechazar con Observaciones*: Devuelve la tarea con feedback oficial para que el docente y el alumno ajusten la entrega.
*   **Gestión de Alumnos y Generación de Códigos QR**: Generación de credenciales QR para enrolamiento ágil de todos los roles (alumnos, docentes, preceptores, validadores).

---

### ⚙️ 4.7. Mantenimiento Técnico y DevSecOps

#### Stack Tecnológico
*   **Frontend**: React 19, TypeScript, Vite 7, Tailwind CSS 4, Lucide Icons, Recharts, Canvas Confetti.
*   **Web3 & Auth**: Pollar Auth (`@pollar/react`), Red Stellar (SDK v14), Soroban Smart Contracts (Rust `#![no_std]`), Passkeys WebAuthn.
*   **Backend**: Supabase (Postgres 15 with RLS and Realtime), Edge Functions en Deno runtime.
*   **Inteligencia Artificial**: Google Gemini 1.5 Flash (Edge Functions) / Gemini Nano (Local AI), Web Speech API, OpenAI `gpt-image-2` con fallback a Pollinations.ai (Flux).
*   **DevSecOps**: ESLint v10 Flat Config, GitHub Actions CI/CD (`deploy-prod.yml`), Vercel Edge Network.

#### Despliegue de Edge Functions (Crítico)
Siempre desplegar funciones de Supabase con el flag `--no-verify-jwt`:
```bash
supabase functions deploy --no-verify-jwt
```

---

### 🧪 4.8. Guía de Pruebas Rápidas (Sandbox v1.55)

| # | Módulo a Probar | Acción del Usuario | Resultado Esperado |
| :-: | :--- | :--- | :--- |
| **1** | **Splash Screen** | Recargar con `F5` en `http://localhost:5173`. | Animación neón fluida con HUD, tips de Stellar y botón "Omitir". |
| **2** | **Login Pollar** | Iniciar sesión sin clave Stellar previa. | Despliegue del asistente Pollar Connect y creación de Smart Account con Trustline Gasless. |
| **3** | **Eduki Assistant & Desafíos** | Iniciar chat con `/` o mic y solicitar consigna. | Apertura automática del formulario maximizado con campos precompletados y auto-minimizado al publicar. |
| **4** | **Asistencia Híbrida** | Conmutar entre Voz Continua y Grilla Táctil en Asistencia. | Reconocimiento por voz con matching fonético Levenshtein y botones táctiles `[P]`, `[A]`, `[T]`, `[J]`. |
| **5** | **Defensa Socrática** | Enviar entrega en *Mis Desafíos*. | Despliegue del modal reflexivo con Eduki, radar de pensamiento (Resiliencia, Profundidad, Originalidad) y notas. |
| **6** | **Pase Cultural $ACT** | Canjear beneficio cultural en el Marketplace. | Quema 1 on-chain ($E4C $\rightarrow$ $ACT) y generación de tarjeta `CulturalPassCard` con QR y código único. |
| **7** | **Terminal POS Web** | Navegar a `/pos` y escanear QR o tipear código `ACT-XXXXXX`. | Verificación del boleto cultural y botón de confirmación de quema definitiva ($ACT $\rightarrow$ Entrada). |
| **8** | **Validación Soroban** | Docente aprueba entrega con Smart Contract. | Verificación de 6 reglas criptográficas y emisión atómica de tokens en Stellar Testnet. |
| **9** | **Libro Doble Partida** | Acceder a *Mis Tokens*. | Cuadre exacto: $\mathbf{Balance} \equiv \mathbf{Ganados} - \mathbf{Canjeados}$ con badges temáticos. |
| **10**| **Auditoría Bóvedas** | En panel de Gobierno/Admin, pulsar "Exportar Auditoría CSV". | Descarga de planilla `.csv` consolidada con estado de divisiones de CABA. |

---

### 🎟️ 4.9. Terminal POS Web de Taquilla Cultural (/pos)

Para posibilitar la validación y canje de entradas y beneficios culturales en comercios físicos, teatros y cines sin requerir instalaciones pesadas de software ni hardware propietario, E4C provee la **Terminal Web POS (`/pos`)** (`POSScannerView.tsx`):

```text
+---------------------------------------------------------------------------------+
|               🎟️ TERMINAL POS DE TAQUILLA CULTURAL — E4C                       |
|  Comercio / Espacio Cultural: Teatro San Martín (CABA)                          |
|                                                                                 |
|  [ 📷 ESCANEAR CÓDIGO QR ]            [ ⌨️ INGRESO MANUAL DE CÓDIGO ]           |
|  +-----------------------------+      +---------------------------------------+ |
|  |     [ Visor de Cámara ]     |      | Ingrese el código alfanumérico:       | |
|  |       Buscando QR...        |      | [ ACT-8F2K91                        ] | |
|  +-----------------------------+      | [ 🔍 Verificar Boleto ]               | |
|                                       +---------------------------------------+ |
|                                                                                 |
|  DETALLES DEL BILLETE VERIFICADO:                                               |
|  • Beneficiario: @pablosebastian (Estudiante Regular CABA)                      |
|  • Función: Obra "El Gran Retablo" — 20:30 hs                                   |
|  • Estado On-Chain: [🟢 ACTIVO - 1 TOKEN $ACT ASIGNADO]                         |
|                                                                                 |
|                [ 🔥 CONFIRMAR Y CANJEAR ENTRADA FÍSICA ]                        |
+---------------------------------------------------------------------------------+
```

1.  **Acceso Web Abierto e Inmediato (`/pos`)**:
    *   Cualquier comercio, cine, teatro o librería adherida al programa accede directamente desde cualquier navegador web en su PC, tablet o celular en la ruta `/pos`.
    *   No requiere descargas desde App Stores, registros complejos ni permisos invasivos.
2.  **Escáner QR por Cámara Nativa (`BarcodeDetector` API)**:
    *   Aprovecha la API nativa del navegador `BarcodeDetector` con soporte de streaming por video (`navigator.mediaDevices.getUserMedia`).
    *   Detecta de forma instantánea el código QR del Pase Cultural presentado por el alumno en su celular o credencial impresa.
3.  **Entrada Manual Alternativa**:
    *   Si la cámara no está disponible o el código QR de la pantalla del alumno está rayado o con bajo brillo, el operador de taquilla puede tipear el código alfanumérico legible (ej: `ACT-8F2K91`).
4.  **Verificación y Quema Definitiva On-Chain (Smart Contract Soroban)**:
    *   Al validar el billete, la pantalla despliega el nombre del estudiante (`@alias`), el evento y la autenticidad del token.
    *   Al pulsar **"Confirmar y Canjear Entrada Física"**, el sistema ejecuta el método `burn_act_for_ticket` en el Smart Contract `E4CCulturalGateway`.
    *   El token $ACT es quemado de forma irreversible en la blockchain Stellar, impidiendo reutilizaciones o fraude, y la taquilla entrega la entrada o libro en mano.

---

### 🛡️ 4.10. Arquitectura de Seguridad y Auditoría de Smart Contracts Soroban (v1.61 — Hackathon Edition)

En la versión **v1.61**, la infraestructura de contratos inteligentes en Stellar/Soroban (`contracts/`) fue sometida a una auditoría y reingeniería técnica exhaustiva para garantizar su solidez, escalabilidad y resiliencia en entornos escolares masivos, con documentación oficial en [`contracts/AUDIT_FINDINGS.md`](contracts/AUDIT_FINDINGS.md) y [`contracts/AUDIT_IMPROVEMENTS.md`](contracts/AUDIT_IMPROVEMENTS.md):

1. **Remediación de Storage y Prevención de 64KB DoS (`E4C-SEC-01`):**
   * *Diagnóstico:* En Soroban, el almacenamiento de instancia (`instance()`) comparte una única entrada de ledger con límite estricto de 64 KB. Almacenar historiales de desafíos, asistencia o pases culturales dentro de la instancia colapsa el contrato cuando la matrícula de alumnos crece.
   * *Solución:* Migración integral de registros dinámicos a `persistent()` ledger storage (`StudentChallenge`, `StudentAttendance`, `Voucher`, `StudentPassport`).
   * *Eficiencia de Renta:* Las cuotas diarias profesor-alumno (`StudentTeacherMint`) fueron migradas a `temporary()` storage, caducando automáticamente tras 7 días sin costo de archivado ni renta a largo plazo.

2. **Blindaje de Control de Acceso en Tokenómica (`E4C-SEC-02`):**
   * *Diagnóstico:* `token_swap` disponía de un método `mint_e4c` que únicamente validaba la firma del llamante sin verificar su rol docente en la institución.
   * *Solución:* Erradicación definitiva de `mint_e4c` en `token_swap`. Principio de responsabilidad única: `token_swap` opera exclusivamente como gateway de canje y quema ($E4C $\rightarrow$ $ACT $\rightarrow$ Ticket), mientras que la emisión legítima está centralizada en `edu_validator` con firma docente registrada, materias y límites de colusión.

3. **Gestión Sistemática de Ciclo de Vida y Renta (TTL - `E4C-SEC-03`):**
   * *Diagnóstico:* Los contratos en Soroban requieren extensión periódica de su tiempo de vida en ledgers (~17.280 ledgers por día). Durante períodos de receso escolar prolongado (vacaciones de invierno o verano), el estado no interactuado corría riesgo de ser archivado por la red.
   * *Solución:* Incorporación de umbrales automáticos (`BUMP_THRESHOLD = 30 días`, `BUMP_TO = 120 días`) en todos los entrypoints de escritura y lectura crítica, garantizando supervivencia indefinida del estado mientras la escuela esté activa.

4. **Manejo Estructurado de Errores Tipados (`E4C-SEC-04`):**
   * Reemplazo de macros `panic!` y `.expect!` por el enum tipado `#[contracterror] pub enum EscrowError` en `partner_escrow`. Permite a los clientes frontend (@stellar/stellar-sdk) capturar códigos de error semánticos (`PartnerNotRegistered`, `InvalidAmount`, `AlreadyInitialized`).

5. **Clarificación Criptográfica en Smart Accounts (`E4C-SEC-05`):**
   * Nomenclatura explícita `SignerKey` para firmas Ed25519 con compatibilidad retroactiva transparente (`PasskeyId`), permitiendo la verificación unificada de firmas de dispositivos hardware y keypairs nativos de Stellar.

6. **Cobertura Integral de Tests Unitarios (`E4C-SEC-06`):**
   * Suites de tests unitarios nativos de Rust (`#[cfg(test)]`) en todos los contratos, simulando contratos SAC de tokens, quema de vouchers en taquilla POS, mitigación de doble gasto y rechazo de validadores no registrados.

---

## 5. Soporte y Solución de Problemas

### ❓ Preguntas Frecuentes (FAQ)

**¿Por qué mis tokens no se acreditan al aprobar un desafío?**
> Para recibir tokens E4C es obligatorio haber vinculado la cuenta mediante **Pollar Auth** o el botón **"Vincular Token E4C"** (establecimiento del Trustline en la red Stellar).

**¿Qué ocurre si la IA comete un error evaluando mi tarea?**
> Gracias al **Framework de Seguridad en IA**, la IA solo emite sugerencias preliminares. El docente siempre revisa la Huella de Razonamiento (Trace) y debe firmar la calificación manualmente (Human-in-the-Loop).

**¿Necesito comprar XLM o criptomonedas para usar Pollar o E4C?**
> **No.** Gracias a la tecnología de Smart Accounts y transacciones patrocinadas (*Gasless*) de Pollar, los alumnos no pagan comisiones de red. E4C es 100% gratuito para las familias.

**¿Los tokens E4C se pueden vender o cambiar por dinero fiat?**
> **No.** En cumplimiento estricto del Art. 32 del Reglamento Escolar de CABA, los tokens E4C son activos pedagógicos no financieros, canjeables exclusivamente por beneficios culturales y formativos provistos por sponsors.

---

### 🚨 Matriz de Errores y Soluciones

| Código / Mensaje de Error | Causa Probable | Procedimiento de Solución |
| :--- | :--- | :--- |
| `tx_no_trustline` (Stellar 400) | El alumno no activó la línea de confianza del token E4C. | Pulsar *"Activar Cuenta Digital"* (Pollar) o *"Vincular Token E4C"* en el panel del estudiante. |
| `tx_bad_seq` | Conflicto de número de secuencia en Stellar. | El sistema reintenta automáticamente con backoff exponencial. Si persiste, recargar la página. |
| `ChallengeAlreadyCompleted` | Intento de revalidar un desafío o registrar asistencia dos veces el mismo día. | Comportamiento normal de seguridad del contrato Soroban (`edu_validator`). |
| `[404 Not Found] models/gemini-1.5-pro...` | Retiro o depreciación de identificadores de modelos antiguos en la API de Google Gemini. | El sistema cuenta con autodescubrimiento dinámico (`ListModels`) hacia Gemini 2.5/3.x y fallback pedagógico local (`buildHeuristicChallenge`), evitando la interrupción del servicio. |

---

### 📖 Glosario de Términos

*   **Pollar Auth / Smart Account**: Cuenta digital educativa no custodial que se crea mediante inicio de sesión social sin requerir frases semilla ni configuraciones técnicas.
*   **Desafío**: Unidad de actividad académica gamificada (reemplaza el concepto de "tarea").
*   **Bóveda Colectiva**: Fondo escolar compartido de la división que acumula tokens por presentismo y desafíos para financiar salidas culturales.
*   **Trustline**: Enlace criptográfico en la red Stellar que autoriza a una cuenta a recibir y almacenar tokens E4C.
*   **Passkey**: Credencial biométrica segura que permite firmar transacciones en Stellar sin exponer claves privadas.
*   **Trace (Huella)**: Registro explicativo y transparente generado por la IA que detalla las razones de una calificación.

---

### 📞 Canales de Soporte

*   **Correo Oficial de Soporte**: `soporte@e4c.education`
*   **Mesa de Ayuda Directa**: Acceso desde el botón `?` en el encabezado de la plataforma.

---

## 🏛️ Marco Normativo: Cumplimiento del Reglamento Escolar de CABA

E4C está diseñado sobre el cumplimiento estricto del **Reglamento Escolar de la Educación Obligatoria de la Ciudad de Buenos Aires (GCBA)**:

*   **Blindaje Cero Especulación y Prevención de Ludopatía (Art. 32)**: E4C es una plataforma **no financiera y 100% educativa**. Prohíbe explícitamente el trading, las criptomonedas volátiles y las interfaces bursátiles en estudiantes.
*   **Exclusión de Cooperadoras Escolares**: Para evitar sobrecarga administrativa, intermediación innecesaria y contratos legales complejos, la plataforma opera directamente bajo la gobernanza de **Direcciones Escolares, Supervisión, Gobierno y Sponsors**, excluyendo a las Cooperadoras del flujo de fondos.
*   **Aportes de Sponsors y Partners**: Todos los fondos de incentivos, beneficios culturales (Cine, Teatro, Libros) y metas colectivas son aportados y fondeados por los **Sponsors y Partners** (empresas, comercios e instituciones adheridas). Los estudiantes ganan tokens E4C mediante su propio mérito académico, cumplimiento de desafíos pedagógicos y presentismo regular.
*   **Financiamiento de Metas de División y Salidas Didácticas (Art. 20, 21, 26, 29 y 31 CABA)**: Las metas colectivas de curso (Salidas Didácticas, visitas culturales y equipamiento escolar) son costeadas directamente por los sponsors y partners del programa, sin requerir aportes familiares, cobro de cuotas ni intermediación de cooperadoras.
