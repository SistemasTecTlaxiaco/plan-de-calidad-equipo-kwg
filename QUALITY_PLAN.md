# Plan de Calidad - StellarTracker dApp

## 1. Introducción

Este documento define el Plan de Calidad para el proyecto **StellarTracker**, una aplicación descentralizada (dApp) desarrollada para la **Stellar Community Fund (SCF)**. La dApp permite a los usuarios crear campañas de donación, realizar contribuciones mediante transacciones en la red Stellar y visualizar el historial y el impacto de los fondos de manera transparente.

El presente plan se basa en los principios de los modelos **MoProSoft** (Nivel de Capacidad 2) y **CMMI** (Nivel 2 - Gestionado), adaptándolos a un entorno ágil y centrado en la comunidad. Su objetivo es asegurar la entrega de un producto funcional, seguro, confiable y que genere valor para el ecosistema Stellar.

## 2. Métricas de Calidad

Las siguientes métricas serán monitoreadas continuamente para evaluar objetivamente la calidad del producto y del proceso de desarrollo.

### 2.1. Métricas de Proceso y Código
| Métrica | Descripción | Objetivo | Herramienta |
| :--- | :--- | :--- | :--- |
| **Cobertura de Pruebas Unitarias** | Porcentaje del código cubierto por pruebas automáticas. | > 85% | Jest, Coverage Reports |
| **Errores Críticos Post-Release** | Número de bugs que impiden el uso core de la app, reportados en producción por versión. | 0 | GitHub Issues |
| **Vulnerabilidades de Seguridad** | Número de vulnerabilidades críticas/altas identificadas en análisis estático. | 0 | SonarQube, OWASP ZAP |
| **Tiempo de Resolución de Bugs** | Tiempo promedio (en horas) entre la reportación de un bug crítico/mayor y su resolución. | < 24 h | GitHub Projects |

### 2.2. Métricas de Producto y Rendimiento
| Métrica | Descripción | Objetivo | Herramienta |
| :--- | :--- | :--- | :--- |
| **Tasa de Éxito de Transacciones** | Porcentaje de transacciones (pagos, donaciones) que se completan con éxito en la red Stellar. | > 99.5% | Stellar Horizon API, Logs |
| **Tiempo de Carga de la Aplicación (LCP)** | Tiempo que tarda el contenido principal en cargarse y ser interactivo. | < 2.5 s | Lighthouse, Web Vitals |
| **Puntuación de Satisfacción del Usuario (CSAT)** | Puntuación promedio obtenida en encuestas de retroalimentación tras la liberación beta. | > 4.2 / 5 | Google Forms, Typeform |

## 3. Procedimientos de Revisión

### 3.1. Revisión de Requisitos y Diseño
- **Revisión de Requisitos:** Todas las historias de usuario (*user stories*) y casos de uso serán revisados en una sesión de planificación (Sprint Planning) con todo el equipo de desarrollo. De ser posible, se invitará a un mentor de la SCF para validar la alineación con los objetivos de la comunidad. Los requisitos se considerarán "aprobados" solo cuando sean **claros, factibles y testeables**.
- **Revisión de Diseño de Arquitectura y Contratos:** El diseño de la arquitectura (frontend, backend) y la lógica de los **Stellar Smart Contracts (Soroban)** será documentado y revisado por un segundo desarrollador senior. El foco estará en identificar riesgos de **seguridad, escalabilidad, costos de transacción e integración** con la red Stellar Testnet/Mainnet.

### 3.2. Revisión de Código (Code Review)
- **Política de Pull Requests (PR):** Todo nuevo código debe ser enviado mediante un PR en GitHub. No se permite el merge directo a las ramas principales (`main`, `develop`).
- **Proceso:** Al menos **un desarrollador** que no sea el autor debe revisar y aprobar el PR. Para cambios críticos (ej: lógica de contratos inteligentes, manejo de claves), se requerirán **dos aprobaciones**.
- **Checklist de Revisión:** La revisión debe verificar:
    - ✅ Funcionalidad correcta y alineada con la historia de usuario.
    - ✅ Ausencia de vulnerabilidades de seguridad conocidas (ej: inyección, manejo incorrecto de seeds).
    - ✅ Cumplimiento de las convenciones de código y estilo definidas (ESLint, Prettier).
    - ✅ Cobertura adecuada de pruebas (unitarias e integración).
    - ✅ Legibilidad y mantenibilidad del código.
    - ✅ Documentación clara de funciones complejas.

## 4. Políticas de Pruebas

Nuestra estrategia de pruebas sigue el modelo de la **Pirámide de Testing** para maximizar la eficiencia y la cobertura.

- **Pruebas Unitarias (Jest, Mocha):** Cubrirán todas las funciones y componentes lógicos individuales de manera aislada (ej: cálculo de comisiones, formateo de direcciones Stellar, validadores de entrada). **Automáticas y obligatorias para cada PR.**.
- **Pruebas de Integración (Cypress, Stellar Testnet):** Verificarán la interacción entre los componentes de la dApp y, crucialmente, con la **red Stellar (Testnet)**. Se probarán flujos completos de extremo a extremo (E2E) como "crear una campaña de donación", "realizar una donación" y "consultar el historial".
- **Pruebas de Seguridad:** Se realizará un escaneo automático semanal de vulnerabilidades web (OWASP Top 10) usando **OWASP ZAP**. Adicionalmente, la lógica de los contratos inteligentes será auditada manualmente en busca de vectores de ataque que puedan leadear a pérdida de fondos.
- **Pruebas de Usabilidad (Beta Testing):** Una versión beta estable será liberada a un grupo selecto de usuarios de la comunidad Stellar. Su feedback cualitativo se recopilará mediante entrevistas y formularios para refinar la experiencia de usuario (UI/UX) antes del lanzamiento mainnet.

## 5. Gestión de la Configuración

### 5.1. Control de Versiones
- **Repositorio:** Todo el código y la documentación se alojan en **GitHub**. El repositorio será público, alineándose con los principios de open source de la SCF.
- **Estrategia de Ramas (Git Flow):**
    - `main`: Representa la versión de producción estable. **Solo recibe merges desde `develop` mediante PR aprobado.**
    - `develop`: Rama de integración para funcionalidades completadas y estables.
    - `feature/*`: Ramas efímeras para desarrollar nuevas funcionalidades. Se fusionan en `develop`.
    - `hotfix/*`: Ramas para corregir urgentemente bugs en producción. Se fusionan en `main` y `develop`.

### 5.2. Gestión de Liberaciones
- **Versionado Semántico (SemVer):** Se seguirá estrictamente el formato `vX.Y.Z` (Major.Minor.Patch).
- **Despliegue Automatizado (CI/CD):** Cada merge a `develop` activará un despliegue automático en un entorno de **Staging (Testnet)**. Cada tag de versión (ej: `v1.2.0`) en `main` activará un despliegue en **Producción (Mainnet)**, el cual requerirá una **aprobación manual final** para confirmar.
- **Comunicación:** Los lanzamientos se anunciarán en el **foro de la SCF** y en las redes sociales del proyecto. Las **Release Notes** en GitHub detallarán los cambios, nuevas funcionalidades y instrucciones de actualización.

## 6. Documentación

La documentación es un entregable de calidad crítico y se gestionará con el mismo rigor que el código. Todo documento debe ser claro, conciso y útil para su audiencia objetivo.

### 6.1. Tipos de Documentación
- **Documentación Técnica Interna:**
    - **README Principal:** Guía de inicio rápido para configurar el entorno de desarrollo, instalar dependencias y ejecutar el proyecto.
    - **Architecture Decision Record (ADR):** Documento que registra las decisiones arquitectónicas importantes, el contexto y las consecuencias.
    - **Documentación de API:** Especificación de los endpoints REST o GraphQL (usando OpenAPI/Swagger).
    - **Guías de Estilo de Código:** Conventions para JavaScript/Soroban, asegurando consistencia en el código.

- **Documentación para el Usuario Final:**
    - **Guía de Usuario:** Documentación clara y con capturas de pantalla que explique cómo usar la dApp: crear una campaña, donar, revisar transacciones.
    - **FAQs (Preguntas Frecuentes):** Respuestas a las dudas comunes sobre el uso de la plataforma, comisiones, y troubleshooting.
    - **Política de Privacidad y Términos de Uso:** Documentos legales que establezcan las reglas de engagement con la aplicación.

### 6.2. Estándares y Proceso
- **La documentación se escribe en Markdown** (.md) para garantizar portabilidad y facilidad de lectura en GitHub.
- **La documentación se almacena en el mismo repositorio** que el código, en una carpeta `/docs`, para mantenerla versionada y sincronizada con cada release.
- **Los cambios en la documentación siguen el mismo proceso de PR y revisión** que el código. Una funcionalidad no se considera terminada hasta que su documentación correspondiente esté completa y aprobada.
- **La documentación se revisa y actualiza** en cada release mayor para reflejar con precisión el estado actual del software.
