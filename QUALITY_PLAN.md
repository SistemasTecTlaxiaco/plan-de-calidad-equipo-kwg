# Plan de Calidad - StellarTracker dApp

## 🎯 Propósito

Este documento establece formalmente el **Plan de Calidad del Producto de Software** para el proyecto **StellarTracker**, una dApp desarrollada para la Stellar Community Fund (SCF). Su propósito es definir los procesos para asegurar que el producto final sea confiable, seguro y cumpla con los objetivos establecidos, alineándose con el modelo **MoProSoft**.

## 📋 Alineación con MoProSoft

Este plan implementa procesos del nivel 2 (Gestionado) de **MoProSoft**:

| Proceso MoProSoft | Acrónimo | Actividades Clave en Este Plan |
| :--- | :--- | :--- |
| **Gestión de Proyectos** | GPROJ | Planificación, seguimiento y control mediante métricas. |
| **Desarrollo y Mantenimiento de Software** | GDSW | Análisis, diseño, construcción, pruebas y documentación. |
| **Gestión de la Calidad del Producto** | GCAL | Definición de métricas, revisiones y auditorías. |
| **Gestión de la Configuración** | GCON | Control de versiones, manejo de cambios y liberaciones. |

---

## 1. Gestión de Proyectos (GPROJ)

### 1.1. Planificación
- Este plan de calidad es un componente integral del plan general del proyecto.
- Se establecen y mantienen los objetivos de calidad, métricas y actividades de aseguramiento.

### 1.2. Seguimiento y Control
- El avance se medirá contra las métricas definidas en la sección 3.
- Las desviaciones activarán acciones correctivas según el proceso **GPROJ - Realizar el seguimiento del plan del proyecto**.

---

## 2. Métricas de Calidad (GCAL)

Las siguientes métricas se monitorizarán para evaluar objetivamente la calidad del producto y del proceso.

| Categoría | Métrica | Objetivo | Herramienta de Medición |
| :--- | :--- | :--- | :--- |
| **Calidad de Producto** | Tasa de Éxito de Transacciones | > 99.5% | Stellar Horizon API |
| | Errores Críticos Post-Liberación | 0 | GitHub Issues |
| **Calidad de Proceso** | Cobertura de Pruebas Unitarias | > 80% | Jest / Coverage Reports |
| | Cumplimiento de Revisiones de Código | 100% de PR revisados | GitHub Insights |
| | Tiempo de Resolución de Bugs (Críticos) | < 24 h | GitHub Projects |

---

## 3. Actividades de Aseguramiento de la Calidad (GCAL)

### 3.1. Revisiones de Pares (Peer Review)
- **Política de Pull Requests (PR):** Todo nuevo código debe ser enviado mediante un PR.
- **Proceso:** Al menos **un desarrollador** que no sea el autor debe revisar y aprobar el PR. Para cambios críticos (ej: lógica de contratos inteligentes, manejo de claves), se requerirán **dos aprobaciones**.
- **Checklist de Revisión Obligatoria:**
    - ✅ Ausencia de vulnerabilidades de seguridad conocidas.
    - ✅ Cumplimiento de las convenciones de código (ESLint, Prettier).
    - ✅ Cobertura adecuada de pruebas (unitarias e integración).
    - ✅ Legibilidad y mantenibilidad del código.
    - ✅ Documentación clara de funciones complejas.

### 3.2. Auditorías de Proceso
- Muestreos periódicos para verificar el cumplimiento de los procesos **GDSW** y **GCON**.
- Realizadas por el Líder de Calidad.

---

## 4. Estrategia de Pruebas (GDSW)

Nuestra estrategia sigue el modelo de la **Pirámide de Testing**.

| Nivel | Tipo de Prueba | Objetivo | Herramienta |
| :--- | :--- | :--- | :--- |
| **1** | Unitarias | Cubrir funciones y componentes lógicos de manera aislada. >80% cobertura. | Jest, Mocha |
| **2** | Integración | Verificar interacción entre componentes y con la red Stellar (Testnet). | Cypress |
| **3** | Seguridad | Escaneo de vulnerabilidades (OWASP Top 10) y auditoría de contratos. | OWASP ZAP |
| **4** | Usabilidad | Feedback cualitativo con usuarios de la comunidad Stellar (Beta Testing). | Typeform |

---

## 5. Gestión de la Configuración (GCON)

### 5.1. Control de Versiones
- **Repositorio:** [URL del Repositorio GitHub]
- **Estrategia de Ramas (Git Flow):**
    - `main`: Versión de producción estable. **Solo recibe merges desde `develop`.**
    - `develop`: Rama de integración para funcionalidades completadas.
    - `feature/*`: Ramas para nuevas funcionalidades.
    - `hotfix/*`: Ramas para corregir bugs críticos en producción.

### 5.2. Gestión de Liberaciones
- **Versionado Semántico (SemVer):** Se seguirá estrictamente el formato `vX.Y.Z`.
- **CI/CD:** 
    - Merge a `develop` → Despliegue automático en **Staging (Testnet)**.
    - Tag en `main` → Despliegue en **Producción (Mainnet)** (con aprobación manual).
- **Comunicación:** Los lanzamientos se anunciarán en el foro de la SCF. Las **Release Notes** en GitHub detallarán los cambios.

---

## 6. Gestión de la Documentación (GDSW / GCON)

La documentación es un elemento de configuración versionado y gestionado.

- **Almacenamiento:** Toda la documentación se encuentra en la carpeta `/docs` del repositorio.
- **Formato:** Todo se escribe en **Markdown** (.md).
- **Proceso:** Los cambios en la documentación siguen el mismo proceso de **PR y revisión** que el código.
- **Tipos de Documentación:**
    - **Técnica:** `README.md`, `ARCHITECTURE.md`, `API.md`.
    - **Usuario Final:** `USER_GUIDE.md`, `FAQs.md`.

---

## ✅ Checklist de Implementación

- [ ] El equipo conoce y comprende este plan de calidad.
- [ ] Las herramientas de medición (Jest, Cypress, OWASP ZAP) están configuradas.
- [ ] Los hooks de pre-commit para linter y pruebas están activos.
- [ ] El pipeline de CI/CD para despliegues en Testnet está configurado.
- [ ] Se ha designado un responsable de liderar las auditorías de proceso (GCAL).

---



