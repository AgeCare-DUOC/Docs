# 📋 Subtareas de Sprint 3 — AgeCare (SPRINT 3 "Bitácora y comunic.")

> **Proyecto:** AgeCare — Suite de Cuidado de Personas Mayores  
> **Asignatura:** APT Capstone — DUOC UC (Sede Antonio Varas)  
> **Contraparte Empresarial:** Alloxentric / Wellq Co  
> **Sprint Jira:** SPRINT 3 "Bitácora y comunic." (ID 10)  
> **Tablero Jira:** `https://capstoneagecare.atlassian.net` (Proyecto `DAC05`)  
> **Período:** 2 semanas (timeboxed)  
> **Versión:** 2.2 (Sincronizado 100% con Jira Software · Claves Reales Verificadas)  
> **Fecha:** Octubre 2026  
> **Marco Metodológico:** Scrum Empírico · Vertical Slicing · DoR INVEST · DoD Integral

---

## 🎯 Resumen General del Sprint

| Métrica | Valor |
|:---|:---|
| **Historias de Usuario Activas** | 7 historias (DAC05-11, 21, 17, 18, 19, 20, 22, 24) |
| **Subtareas Totales en Jira** | 34 subtareas sincronizadas y enriquecidas |
| **Puntos Totales Comprometidos** | 41 puntos (Escala Fibonacci: 1, 2, 3, 5, 8, 13) |
| **Velocity de Referencia Sprint 2** | 32 puntos completados (100% Done) |
| **Distribución de Capas Técnicas** | Frontend (Flutter) · Backend (FastAPI) · Base de Datos (PostgreSQL/Alembic) · Infraestructura (Azure) · QA · DoD / Git |
| **Integrantes del Equipo** | César Gacitúa · Claudia Iosue · Franco Barra · Felipe Varas |

---

## 📌 Estado de Trazabilidad en Jira Software

Todas las subtareas del backlog de Sprint 3 han sido completadas y enriquecidas directamente en el tablero Jira con:
1. **Descripción Técnica del Trabajo:** Propósito específico y alcance dentro del corte vertical.
2. **Criterios de Aceptación Técnicos Granulares (DoD):** Checklist verificable por capa de ingeniería para respaldar la entrega con cero defectos y la evaluación individual de DUOC UC.

---

## 1. DAC05-11 — Pantalla de inicio con semáforo de bienestar (3 pts)

* **Épica Padre:** `DAC05-100` (Vitals, wearable y semáforo)
* **Responsable de Historia:** César Gacitúa
* **Fórmula INVEST:** Como familiar, quiero ver un semáforo de bienestar en la pantalla de inicio que indique si mi adulto mayor se encuentra bien, para saber de un vistazo si requiere mi atención inmediata.
* **Criterios de Aceptación BDD (Negocio):**
  * *Dado que* el familiar ha iniciado sesión correctamente, *cuando* accede a la pantalla de inicio, *entonces* visualiza un semáforo con estado: verde (`ok`), amarillo (`warning`) o rojo (`critical`).
  * *Dado que* existen signos vitales registrados del paciente, *cuando* el familiar consulta el semáforo, *entonces* el estado refleja la última agregación de signos vitales.
  * *Dado que* no hay datos de signos vitales recientes, *cuando* el familiar abre la pantalla, *entonces* el sistema muestra un estado "Sin datos recientes" con opción de sincronizar.

### 📊 Tabla Resumen de Subtareas (Jira DAC05)

| Clave Jira | Título | Capa | Descripción | Asignado | Estimación |
|:---|:---|:---|:---|:---|:---|
| **DAC05-177** | UI: Pantalla semáforo bienestar (Flutter) | Frontend | Crear pantalla de inicio con widget semáforo que muestra estado de bienestar del paciente conectado a endpoint de vitales. Incluir indicadores visuales para cada estado y mensaje de "sin datos" cuando no haya lecturas. | César Gacitúa | 2 pts |
| **DAC05-178** | API: Endpoint GET /api/v1/patients/{id}/wellbeing (FastAPI) | Backend | Implementar endpoint REST asíncrono que calcule y retorne el semáforo de bienestar basado en signos vitales recientes y umbrales configurados. Retornar estado (ok/warning/critical) con valores de signos vitales. | César Gacitúa | 3 pts |
| **DAC05-179** | DB: Modelo y migración para lecturas de signos vitales (PostgreSQL) | Base de Datos | Crear migración Alembic para tabla vital_readings con columnas: id, patient_id, vital_type, value, measured_at, source, created_at. Incluir modelo ORM SQLAlchemy e índices en patient_id y measured_at. | César Gacitúa | 2 pts |
| **DAC05-180** | QA: flutter test + flutter analyze semáforo bienestar | QA | Ejecutar suite completa de pruebas unitarias y de widget para el módulo de semáforo. Verificar que flutter analyze no tenga advertencias ni errores. | Felipe Varas | 2 pts |
| **DAC05-181** | PR: Peer review y merge a main - Semáforo bienestar | DoD / Git | Crear Pull Request en GitHub hacia rama main, obtener aprobación de al menos un revisor técnico, realizar Squash and Merge una vez aprobado. Commit con formato DAC05-11: descripción corta en español. | César Gacitúa | 1 pt |

### 🔬 Especificación y Criterios de Aceptación Granulares por Subtarea

#### `DAC05-177` — UI: Pantalla semáforo bienestar (Flutter)
* **Capa:** Frontend | **Asignado:** César Gacitúa | **Estimación:** 2 pts
* **Descripción del Trabajo:** Crear pantalla de inicio con widget semáforo que muestra el estado de bienestar del paciente conectado al endpoint de vitales. Incluir indicadores visuales para cada estado y mensaje de "sin datos" cuando no haya lecturas.
* **Criterios de Aceptación Técnicos Granulares (DoD):**
  - [ ] Widget principal del semáforo implementado según el design system (Material 3) con soporte para 3 estados visuales: Verde (`ok`), Amarillo (`warning`) y Rojo (`critical`), con ícono representativo y contraste accesible.
  - [ ] Implementación de estado vacío (*empty state*) informativo ("Sin datos de signos vitales disponibles") y estado de carga reactivo (*shimmer effect* o indicador circular centrado) consumiendo el provider de Riverpod.
  - [ ] Manejo de errores en capa de presentación: si el endpoint falla, muestra widget de reintento (*Retry Button*) sin romper el renderizado.
  - [ ] Diseño adaptable (*responsive*) probado en resoluciones móviles estándar y web sin errores de *overflow* (`RenderFlex`).
  - [ ] Código ubicado en arquitectura limpia bajo `presentation/screens/home/` y `presentation/widgets/wellbeing/`, superando `flutter analyze` con 0 errores y 0 warnings.

#### `DAC05-178` — API: Endpoint GET /api/v1/patients/{id}/wellbeing (FastAPI)
* **Capa:** Backend | **Asignado:** César Gacitúa | **Estimación:** 3 pts
* **Descripción del Trabajo:** Implementar endpoint REST asíncrono que calcule y retorne el semáforo de bienestar basado en signos vitales recientes y umbrales configurados. Retornar estado (ok/warning/critical) con valores de signos vitales.
* **Criterios de Aceptación Técnicos Granulares (DoD):**
  - [ ] Endpoint `GET /api/v1/patients/{id}/wellbeing` implementado en FastAPI con controlador asíncrono y sesión inyectada de `asyncpg`.
  - [ ] Esquema de respuesta Pydantic v2 estricto que retorne: `patient_id` (UUID), `status` (`ok` | `warning` | `critical` | `no_data`), `score` (float/int), `summary` (string descriptivo) y `latest_readings` (lista de signos vitales evaluados con timestamp ISO-8601).
  - [ ] Reglas de cálculo del semáforo: evalúa lecturas de las últimas 24 horas; si hay al menos una lectura crítica activa retorna `critical`; si hay lecturas en umbral de advertencia retorna `warning`; si todo está en rango seguro retorna `ok`.
  - [ ] Manejo estándar de códigos HTTP: `200 OK` con payload JSON; `401 Unauthorized` si no hay token Bearer válido; `403 Forbidden` si el usuario autenticado no pertenece a la familia del paciente; `404 Not Found` si el paciente no existe.
  - [ ] Documentación OpenAPI/Swagger enriquecida con descripciones de campos y respuestas de ejemplo.

#### `DAC05-179` — DB: Modelo y migración para lecturas de signos vitales (PostgreSQL)
* **Capa:** Base de Datos | **Asignado:** César Gacitúa | **Estimación:** 2 pts
* **Descripción del Trabajo:** Crear migración Alembic para tabla vital_readings con columnas: id, patient_id, vital_type, value, measured_at, source, created_at. Incluir modelo ORM SQLAlchemy e índices en patient_id y measured_at.
* **Criterios de Aceptación Técnicos Granulares (DoD):**
  - [ ] Migración Alembic generada y verificada bidireccionalmente (`alembic upgrade head` y `alembic downgrade -1`) para la tabla `vital_readings`.
  - [ ] Columnas requeridas: `id` (UUID, PK), `patient_id` (UUID, FK a `patients(id)` ON DELETE CASCADE), `vital_type` (VARCHAR(50), ej: `heart_rate`, `blood_pressure_sys`, `spo2`, `temperature`), `value` (NUMERIC(6,2)), `unit` (VARCHAR(20)), `measured_at` (TIMESTAMPTZ), `source` (VARCHAR(50), ej: `manual`, `wearable`), `created_at` (TIMESTAMPTZ DEFAULT now()).
  - [ ] Índices compuestos B-tree creados para optimización de consultas: índice en `(patient_id, measured_at DESC)` e índice en `(patient_id, vital_type)`.
  - [ ] Modelo ORM SQLAlchemy 2.0 con tipado estricto y relación mapeada con el modelo `Patient`.

#### `DAC05-180` — QA: flutter test + flutter analyze semáforo bienestar
* **Capa:** QA | **Asignado:** Felipe Varas | **Estimación:** 2 pts
* **Descripción del Trabajo:** Ejecutar suite completa de pruebas unitarias y de widget para el módulo de semáforo. Verificar que flutter analyze no tenga advertencias ni errores.
* **Criterios de Aceptación Técnicos Granulares (DoD):**
  - [ ] Pruebas unitarias de Riverpod StateNotifier/Notifier que validen las transiciones de estado: `AsyncLoading` → `AsyncData` (estados verde, amarillo, rojo) y `AsyncError`.
  - [ ] Pruebas de widget (*Widget Tests*) verificando que el semáforo muestre el color e ícono correspondiente según el estado provisto por el mock del servicio.
  - [ ] Verificación de prueba de accesibilidad (contraste de color y semántica de pantalla para lectores de voz).
  - [ ] Ejecución de `flutter test` con 100% de aserciones en verde y suite de análisis `flutter analyze` limpia (cero lints, cero advertencias).

#### `DAC05-181` — PR: Peer review y merge a main - Semáforo bienestar
* **Capa:** DoD / Git | **Asignado:** César Gacitúa | **Estimación:** 1 pt
* **Descripción del Trabajo:** Crear Pull Request en GitHub hacia rama main, obtener aprobación de al menos un revisor técnico, realizar Squash and Merge una vez aprobado. Commit con formato DAC05-11: descripción corta en español.
* **Criterios de Aceptación Técnicos Granulares (DoD):**
  - [ ] Rama de trabajo nombrada estrictamente como `feature/DAC05-11-semaforo-bienestar`.
  - [ ] Commits atómicos siguiendo la convención: `DAC05-11: <descripción en español>` (ej: `DAC05-11: Crear endpoint GET bienestar`).
  - [ ] Pull Request en GitHub con descripción detallada del cambio, capturas de pantalla de la UI, respuesta cURL de prueba y checklist DoD completado.
  - [ ] Aprobación explícita mediante *Peer Review* de al menos un compañero de equipo (`@cl.iosue`, `@FRANCO . BARRA BARRA` o `@f.varasc`).
  - [ ] Integración exitosa a rama `main` mediante *Squash and Merge*, dejando el issue de Jira actualizado con comentario de cierre y commit SHA.

---

## 2. DAC05-21 — Check-in diario de la cuidadora (5 pts)

* **Épica Padre:** `DAC05-103` (Bitácora de cuidado)
* **Responsable de Historia:** César Gacitúa
* **Fórmula INVEST:** Como cuidadora, quiero registrar mi check-in al inicio del turno y ver mi lista de tareas diarias, para llevar un control organizado del cuidado del adulto mayor y asegurar la continuidad operativa.
* **Criterios de Aceptación BDD (Negocio):**
  * *Dado que* la cuidadora inicia su jornada laboral, *cuando* presiona el botón de check-in, *entonces* el sistema registra la entrada con timestamp inmutable y georreferencia opcional.
  * *Dado que* existe un plan diario de cuidado, *cuando* la cuidadora accede a su pantalla principal, *entonces* visualiza las tareas clasificadas en: pendientes, completadas y omitidas.
  * *Dado que* la cuidadora marca una tarea como realizada, *cuando* confirma la acción, *entonces* el estado cambia inmediatamente a completada con registro de hora.

### 📊 Tabla Resumen de Subtareas (Jira DAC05)

| Clave Jira | Título | Capa | Descripción | Asignado | Estimación |
|:---|:---|:---|:---|:---|:---|
| **DAC05-201** | UI: Pantalla check-in y lista de tareas diarias (Flutter) | Frontend | Crear pantalla con botón para registrar entrada del turno con fecha y hora, y lista de tareas diarias del paciente con estados (pendientes, completadas, omitidas). Permitir marcar tareas como completadas. | César Gacitúa | 2 pts |
| **DAC05-202** | API: Endpoint check-in y tareas diarias (FastAPI) | Backend | Implementar endpoint POST para registro de check-in de cuidadora y endpoint GET para listar tareas diarias del paciente. Incluir validación de membresía y manejo de errores estándar. | César Gacitúa | 2 pts |
| **DAC05-203** | DB: Migración tablas check_in y daily_tasks (PostgreSQL) | Base de Datos | Crear migración Alembic para tablas check_in (id, cuidadora_id, paciente_id, fecha_entrada, hora_entrada) y daily_tasks (id, paciente_id, tarea, estado, fecha_programada, fecha_completado). Índices en cuidadora_id, paciente_id y fechas. | César Gacitúa | 2 pts |
| **DAC05-204** | QA: flutter test + flutter analyze check-in | QA | Ejecutar suite completa de pruebas unitarias y de widget para el módulo de check-in. Verificar que flutter analyze no tenga advertencias ni errores. | Felipe Varas | 2 pts |
| **DAC05-205** | PR: Peer review y merge a main - Check-in diario | DoD / Git | Crear Pull Request en GitHub hacia rama main con implementación de check-in diario. Obtener aprobación de al menos un revisor técnico y realizar Squash and Merge una vez aprobado. | César Gacitúa | 1 pt |

### 🔬 Especificación y Criterios de Aceptación Granulares por Subtarea

#### `DAC05-201` — UI: Pantalla check-in y lista de tareas diarias (Flutter)
* **Capa:** Frontend | **Asignado:** César Gacitúa | **Estimación:** 2 pts
* **Descripción del Trabajo:** Crear pantalla con botón para registrar entrada del turno con fecha y hora, y lista de tareas diarias del paciente con estados (pendientes, completadas, omitidas). Permitir marcar tareas como completadas.
* **Criterios de Aceptación Técnicos Granulares (DoD):**
  - [ ] Botón de acción prominente "Registrar Entrada de Turno" con confirmación háptica/visual y deshabilitación inmediata tras el registro exitoso del día.
  - [ ] Lista interactiva de tareas diarias agrupadas por franja horaria (Mañana, Tarde, Noche) con selector de estado (Completar / Omitir con motivo).
  - [ ] Actualización optimista de la UI al marcar una tarea, sincronizando el estado con el backend mediante Riverpod Provider.
  - [ ] Indicador visual del turno actual activo: nombre de la cuidadora en turno y tiempo transcurrido desde el check-in.
  - [ ] Interfaz completamente adaptada para usabilidad en una sola mano y sin advertencias en `flutter analyze`.

#### `DAC05-202` — API: Endpoint check-in y tareas diarias (FastAPI)
* **Capa:** Backend | **Asignado:** César Gacitúa | **Estimación:** 2 pts
* **Descripción del Trabajo:** Implementar endpoint POST para registro de check-in de cuidadora y endpoint GET para listar tareas diarias del paciente. Incluir validación de membresía y manejo de errores estándar.
* **Criterios de Aceptación Técnicos Granulares (DoD):**
  - [ ] Endpoint `POST /api/v1/caregivers/check-in` que reciba `patient_id`, `notes` (opcional), capture automáticamente el `caregiver_id` desde el token JWT y valide que no exista un check-in activo no cerrado. Retorna código `201 Created`.
  - [ ] Endpoint `GET /api/v1/patients/{id}/daily-tasks?date=YYYY-MM-DD` que retorne lista ordenada de tareas del día con sus estados (`pending`, `completed`, `skipped`). Retorna `200 OK`.
  - [ ] Endpoint `PATCH /api/v1/daily-tasks/{task_id}` para actualizar estado de tarea con timestamp de ejecución y notas de omisión si aplica.
  - [ ] Control estricto de roles: solo usuarios con rol `caregiver` o `admin` pueden registrar check-in y modificar tareas; familiares tienen acceso de solo lectura (`GET`). Códigos `403 Forbidden` en caso no autorizado.

#### `DAC05-203` — DB: Migración tablas check_in y daily_tasks (PostgreSQL)
* **Capa:** Base de Datos | **Asignado:** César Gacitúa | **Estimación:** 2 pts
* **Descripción del Trabajo:** Crear migración Alembic para tablas check_in (id, cuidadora_id, paciente_id, fecha_entrada, hora_entrada) y daily_tasks (id, paciente_id, tarea, estado, fecha_programada, fecha_completado). Índices en cuidadora_id, paciente_id y fechas.
* **Criterios de Aceptación Técnicos Granulares (DoD):**
  - [ ] Migración Alembic ejecutable sin conflictos para crear las tablas `caregiver_checkins` y `daily_tasks`.
  - [ ] Esquema `caregiver_checkins`: `id` (UUID, PK), `caregiver_id` (UUID, FK a `users(id)`), `patient_id` (UUID, FK a `patients(id)`), `check_in_at` (TIMESTAMPTZ NOT NULL), `check_out_at` (TIMESTAMPTZ NULL), `notes` (TEXT), `created_at` (TIMESTAMPTZ).
  - [ ] Esquema `daily_tasks`: `id` (UUID, PK), `patient_id` (UUID, FK a `patients(id)`), `title` (VARCHAR(150) NOT NULL), `category` (VARCHAR(50)), `scheduled_time` (TIME), `status` (VARCHAR(20) DEFAULT 'pending'), `completed_at` (TIMESTAMPTZ NULL), `completed_by` (UUID, FK a `users(id)` NULL).
  - [ ] Constraints: restricción CHECK en `daily_tasks.status` para permitir únicamente `('pending', 'completed', 'skipped')`. Índices en `(patient_id, scheduled_time)` y `(caregiver_id, check_in_at)`.

#### `DAC05-204` — QA: flutter test + flutter analyze check-in
* **Capa:** QA | **Asignado:** Felipe Varas | **Estimación:** 2 pts
* **Descripción del Trabajo:** Ejecutar suite completa de pruebas unitarias y de widget para el módulo de check-in. Verificar que flutter analyze no tenga advertencias ni errores.
* **Criterios de Aceptación Técnicos Granulares (DoD):**
  - [ ] Pruebas unitarias de modelos Dart (serialización y deserialización JSON de `CheckInModel` y `DailyTaskModel`).
  - [ ] Pruebas de integración de widget: simular flujo de tap en "Registrar Entrada", verificar cambio visual de estado del botón y renderizado de la lista de tareas.
  - [ ] Pruebas de manejo de errores de red (simular error HTTP 500 y verificar que se muestre SnackBar amigable sin congelar la app).
  - [ ] Cobertura de pruebas unitarias sobre el notifier superior al 85% y `flutter analyze` con cero defectos.

#### `DAC05-205` — PR: Peer review y merge a main - Check-in diario
* **Capa:** DoD / Git | **Asignado:** César Gacitúa | **Estimación:** 1 pt
* **Descripción del Trabajo:** Crear Pull Request en GitHub hacia rama main con implementación de check-in diario. Obtener aprobación de al menos un revisor técnico y realizar Squash and Merge una vez aprobado.
* **Criterios de Aceptación Técnicos Granulares (DoD):**
  - [ ] Branch oficial: `feature/DAC05-21-checkin-diario-tareas`.
  - [ ] Commits atómicos: `DAC05-21: <mensaje>` documentando endpoints, migración y componentes visuales.
  - [ ] PR en GitHub con evidencia de ejecución de pruebas en verde y descripción del modelo relacional introducido.
  - [ ] Aprobación de *Peer Review* por al menos un integrante del equipo (`@f.varasc` o `@ce.gacitua`).
  - [ ] Fusión mediante *Squash and Merge* y actualización de estado en Jira.

---

## 3. DAC05-17 — Centro de alertas (5 pts)

* **Épica Padre:** `DAC05-102` (Alertas críticas y SOS)
* **Responsable de Historia:** Claudia Iosue
* **Fórmula INVEST:** Como familiar o cuidadora, quiero ver un centro de alertas con el historial cronológico de notificaciones y filtros por severidad, para estar al tanto de eventos críticos y coordinar acciones oportunas.
* **Criterios de Aceptación BDD (Negocio):**
  * *Dado que* existen alertas registradas en el sistema, *cuando* el usuario abre el centro de alertas, *entonces* visualiza la lista en orden cronológico inverso con etiquetas de severidad y tipo.
  * *Dado que* hay una alerta crítica no leída, *cuando* el usuario ingresa al módulo, *entonces* se destaca con contraste rojo y ofrece acción rápida para marcarla como atendida/leída.
  * *Dado que* el usuario filtra por tipo de alerta (ej: `caída`, `medicamento`, `vitales`), *cuando* pulsa el filtro, *entonces* el listado se acota instantáneamente a dicha categoría.

### 📊 Tabla Resumen de Subtareas (Jira DAC05)

| Clave Jira | Título | Capa | Descripción | Asignado | Estimación |
|:---|:---|:---|:---|:---|:---|
| **DAC05-187** | UI: Pantalla centro de alertas con historial (Flutter) | Frontend | Crear pantalla que muestre historial cronológico de alertas con tipo, estado y fecha. Incluir indicador visual para alertas críticas, opción de marcar como leída, y filtros por tipo de alerta. | Claudia Iosue | 2 pts |
| **DAC05-188** | API: Endpoint GET alertas con historial (FastAPI) | Backend | Implementar endpoint que retorne lista de alertas del paciente filtradas por miembro autorizado, con paginación y filtro por tipo de alerta. | Claudia Iosue | 2 pts |
| **DAC05-189** | DB: Modelo y migración tabla alerts (PostgreSQL) | Base de Datos | Crear migración Alembic para tabla alerts con campos: tipo, severidad, mensaje, fecha_creacion, estado, paciente_id. Incluir modelo ORM e índices en paciente_id y fecha_creacion. | Claudia Iosue | 2 pts |
| **DAC05-190** | QA: pytest + flutter analyze centro de alertas | QA | Ejecutar pruebas backend (pytest) y frontend (flutter test + flutter analyze) del módulo de alertas. Verificar que no haya advertencias ni errores. | Felipe Varas | 2 pts |
| **DAC05-191** | PR: Peer review y merge a main - Centro de alertas | DoD / Git | Crear Pull Request en GitHub hacia rama main, obtener aprobación de al menos un revisor técnico, realizar Squash and Merge una vez aprobado. Commit con formato DAC05-17: descripción corta en español. | Claudia Iosue | 1 pt |

### 🔬 Especificación y Criterios de Aceptación Granulares por Subtarea

#### `DAC05-187` — UI: Pantalla centro de alertas con historial (Flutter)
* **Capa:** Frontend | **Asignado:** Claudia Iosue | **Estimación:** 2 pts
* **Descripción del Trabajo:** Crear pantalla que muestre historial cronológico de alertas con tipo, estado y fecha. Incluir indicador visual para alertas críticas, opción de marcar como leída, y filtros por tipo de alerta.
* **Criterios de Aceptación Técnicos Granulares (DoD):**
  - [ ] Pantalla `AlertsCenterScreen` con lista infinita paginada o pull-to-refresh, mostrando tarjetas de alerta diferenciadas por color de severidad: `critical` (rojo), `warning` (amarillo/naranja), `info` (azul).
  - [ ] Barra superior con chips de filtrado interactivo: "Todas", "Críticas", "Medicamentos", "Signos Vitales" y "Caídas".
  - [ ] Acción de deslizar o botón explícito para "Marcar como leída", actualizando el contador global de notificaciones no leídas en el badge de la barra de navegación.
  - [ ] Vista de detalle de alerta al presionar una tarjeta, mostrando fecha exacta, descripción, parámetros detonantes y usuario que la atendió.
  - [ ] `flutter analyze` sin advertencias y widgets modulares desacoplados en `presentation/screens/alerts/`.

#### `DAC05-188` — API: Endpoint GET alertas con historial (FastAPI)
* **Capa:** Backend | **Asignado:** Claudia Iosue | **Estimación:** 2 pts
* **Descripción del Trabajo:** Implementar endpoint que retorne lista de alertas del paciente filtradas por miembro autorizado, con paginación y filtro por tipo de alerta.
* **Criterios de Aceptación Técnicos Granulares (DoD):**
  - [ ] Endpoint `GET /api/v1/patients/{id}/alerts` con soporte de parámetros query: `severity` (opcional), `type` (opcional), `is_read` (bool opcional), `limit` (default 20, max 100) y `offset` (default 0).
  - [ ] Endpoint `PATCH /api/v1/alerts/{alert_id}/read` para actualizar el estado de lectura registrando el `read_at` y `read_by_user_id`.
  - [ ] Validación de seguridad multi-inquilino (*multi-tenant* familiar): verifica que el usuario solicitante tenga vínculo activo con el `patient_id` en la tabla de membresías familiares o cuidadores asignados.
  - [ ] Respuestas estructuradas con Pydantic v2: modelo `AlertResponse` incluyendo metadata de paginación (`total`, `has_more`). Retorno de `200 OK` y `403 Forbidden` si no hay acceso.

#### `DAC05-189` — DB: Modelo y migración tabla alerts (PostgreSQL)
* **Capa:** Base de Datos | **Asignado:** Claudia Iosue | **Estimación:** 2 pts
* **Descripción del Trabajo:** Crear migración Alembic para tabla alerts con campos: tipo, severidad, mensaje, fecha_creacion, estado, paciente_id. Incluir modelo ORM e índices en paciente_id y fecha_creacion.
* **Criterios de Aceptación Técnicos Granulares (DoD):**
  - [ ] Migración Alembic para la tabla `alerts` con reversibilidad garantizada.
  - [ ] Atributos requeridos: `id` (UUID, PK), `patient_id` (UUID, FK a `patients(id)`), `alert_type` (VARCHAR(50) NOT NULL, ej: `fall_detected`, `vital_out_of_range`, `sos_button`, `medication_missed`), `severity` (VARCHAR(20) NOT NULL), `title` (VARCHAR(150)), `message` (TEXT NOT NULL), `is_read` (BOOLEAN DEFAULT FALSE), `read_at` (TIMESTAMPTZ NULL), `created_at` (TIMESTAMPTZ DEFAULT now()).
  - [ ] Constraints e índices: CHECK en `severity IN ('info', 'warning', 'critical')`. Índices en `(patient_id, created_at DESC)` y `(patient_id, is_read, severity)`.
  - [ ] Modelo SQLAlchemy con tipado moderno (`Mapped` y `mapped_column`).

#### `DAC05-190` — QA: pytest + flutter analyze centro de alertas
* **Capa:** QA | **Asignado:** Felipe Varas | **Estimación:** 2 pts
* **Descripción del Trabajo:** Ejecutar pruebas backend (pytest) y frontend (flutter test + flutter analyze) del módulo de alertas. Verificar que no haya advertencias ni errores.
* **Criterios de Aceptación Técnicos Granulares (DoD):**
  - [ ] Suite de pruebas backend con `pytest`: test de endpoint `GET /alerts` validando paginación, filtros por severidad y validación de permisos de membresía (esperando 403 para usuarios no autorizados).
  - [ ] Test unitario de `PATCH /alerts/{id}/read` asegurando mutación correcta de `is_read` y timestamp.
  - [ ] Pruebas en frontend (`flutter test`) verificando la reactividad del filtro por chips y la actualización del badge.
  - [ ] Ejecución de `ruff check .` en backend y `flutter analyze` en frontend con 100% de éxito.

#### `DAC05-191` — PR: Peer review y merge a main - Centro de alertas
* **Capa:** DoD / Git | **Asignado:** Claudia Iosue | **Estimación:** 1 pt
* **Descripción del Trabajo:** Crear Pull Request en GitHub hacia rama main, obtener aprobación de al menos un revisor técnico, realizar Squash and Merge una vez aprobado. Commit con formato DAC05-17: descripción corta en español.
* **Criterios de Aceptación Técnicos Granulares (DoD):**
  - [ ] Rama: `feature/DAC05-17-centro-alertas-historial`.
  - [ ] Formato de commits: `DAC05-17: <descripción corta en español>`.
  - [ ] Pull Request con evidencia de cobertura de pruebas unitarias y descripción de endpoints.
  - [ ] Revisión técnica aprobada por `@cl.iosue` o `@ce.gacitua`.
  - [ ] Squash and Merge a `main` con trazabilidad completa a Jira.

---

## 4. DAC05-18 — Flujo crítico ante caídas (5 pts)

* **Épica Padre:** `DAC05-102` (Alertas críticas y SOS)
* **Responsable de Historia:** Franco Barra
* **Fórmula INVEST:** Como cuidadora o familiar, quiero recibir una notificación inmediata de máxima prioridad cuando se detecte una caída del adulto mayor, para reaccionar al instante y verificar su integridad física.
* **Criterios de Aceptación BDD (Negocio):**
  * *Dado que* el wearable o dispositivo envía una señal de caída, *cuando* el sistema recibe la trama, *entonces* genera una alerta crítica y despacha notificaciones push a todos los cuidadores y familiares activos en menos de 5 segundos.
  * *Dado que* se detona la alerta en el móvil, *cuando* el receptor abre la notificación, *entonces* la app despliega la pantalla de acción inmediata con botones de llamada de emergencia y descarte de falsa alarma.
  * *Dado que* transcurre el tiempo de gracia (ej: 60 segundos) sin confirmación de atención, *cuando* expira el temporizador, *entonces* el sistema escala la alerta al contacto secundario configurado.

### 📊 Tabla Resumen de Subtareas (Jira DAC05)

| Clave Jira | Título | Capa | Descripción | Asignado | Estimación |
|:---|:---|:---|:---|:---|:---|
| **DAC05-84** | UI de pantalla de acción inmediata | Frontend | Pantalla existente para acción inmediata ante detección de caída. | Franco Barra | 0 pts |
| **DAC05-85** | Lógica de botones de llamada (cuidadora/emergencias) | Frontend | Lógica existente de botones de llamada (cuidadora/emergencias). | Franco Barra | 0 pts |
| **DAC05-86** | Probar flujo alcanzable con app cerrada | QA | Prueba existente de flujo con app cerrada. | Franco Barra | 0 pts |
| **DAC05-192** | API: Endpoint POST alertas SOS (FastAPI) | Backend | Implementar endpoint que reciba evento de caída del wearable y genere alerta crítica en tiempo real. | Franco Barra | 3 pts |
| **DAC05-193** | Infra: Notificación push SOS (FCM/APNs - Azure) | Infraestructura | Configurar notificación push vía FCM/APNs para alertas de caída, integrada con Azure. | Franco Barra | 3 pts |
| **DAC05-194** | QA: flutter test + pytest E2E botón SOS | QA | Ejecutar pruebas end-to-end del flujo de caída: detección → alerta → notificación push. | Felipe Varas | 3 pts |
| **DAC05-195** | PR: Peer review y merge a main - Botón SOS | DoD / Git | Crear Pull Request en GitHub hacia rama main, obtener aprobación de al menos un revisor técnico, realizar Squash and Merge una vez aprobado. | Franco Barra | 1 pt |

### 🔬 Especificación y Criterios de Aceptación Granulares por Subtarea

#### `DAC05-84` — UI de pantalla de acción inmediata
* **Capa:** Frontend | **Asignado:** Franco Barra | **Estimación:** 0 pts
* **Descripción del Trabajo:** Pantalla existente para acción inmediata ante detección de caída.
* **Criterios de Aceptación Técnicos Granulares (DoD):**
  - [ ] Verificar que la pantalla existente `ImmediateActionScreen` se enlace correctamente con el payload de la notificación push de caída recibida.
  - [ ] Comprobar despliegue visual de alarma con fondo de alerta de alta visibilidad, sonido de notificación prioritario y datos del adulto mayor (nombre, dirección y última ubicación registrada).

#### `DAC05-85` — Lógica de botones de llamada (cuidadora/emergencias)
* **Capa:** Frontend | **Asignado:** Franco Barra | **Estimación:** 0 pts
* **Descripción del Trabajo:** Lógica existente de botones de llamada (cuidadora/emergencias).
* **Criterios de Aceptación Técnicos Granulares (DoD):**
  - [ ] Botón de llamada directa a emergencias (131 SAMU / 133 Carabineros en Chile o contacto médico) funcional utilizando `url_launcher` con esquema `tel:`.
  - [ ] Botón de contacto directo a cuidadora en turno con marcado telefónico inmediato.
  - [ ] Botón de "Confirmar Falsa Alarma" que registre el descarte en backend con justificación obligatoria.

#### `DAC05-86` — Probar flujo alcanzable con app cerrada
* **Capa:** QA | **Asignado:** Franco Barra | **Estimación:** 0 pts
* **Descripción del Trabajo:** Prueba existente de flujo con app cerrada.
* **Criterios de Aceptación Técnicos Granulares (DoD):**
  - [ ] Comprobar que ante la llegada de la notificación push de alta prioridad, la app pueda despertar desde estado cerrado (*terminated*) o segundo plano (*background*) y redirigir directamente a la pantalla de acción inmediata.
  - [ ] Validación documentada en entorno de pruebas (emulador Android / dispositivo físico).

#### `DAC05-192` — API: Endpoint POST alertas SOS (FastAPI)
* **Capa:** Backend | **Asignado:** Franco Barra | **Estimación:** 3 pts
* **Descripción del Trabajo:** Implementar endpoint que reciba evento de caída del wearable y genere alerta crítica en tiempo real.
* **Criterios de Aceptación Técnicos Granulares (DoD):**
  - [ ] Endpoint `POST /api/v1/alerts/critical-event` protegido por API Key de dispositivo o token Bearer.
  - [ ] Payload JSON Pydantic v2: `patient_id` (UUID), `event_type` (`fall_detected` | `sos_manual`), `timestamp` (ISO-8601), `confidence_level` (float 0.0-1.0), `telemetry_snapshot` (objeto opcional con acelerómetro o coordenadas GPS).
  - [ ] El endpoint inserta la alerta crítica en la base de datos de forma transaccional y dispara la tarea asíncrona de notificación push en segundo plano (*BackgroundTasks* o cola de mensajería).
  - [ ] Retorna `201 Created` con el `alert_id` generado en menos de 200 ms para asegurar baja latencia en situaciones de emergencia.

#### `DAC05-193` — Infra: Notificación push SOS (FCM/APNs - Azure)
* **Capa:** Infraestructura | **Asignado:** Franco Barra | **Estimación:** 3 pts
* **Descripción del Trabajo:** Configurar notificación push vía FCM/APNs para alertas de caída, integrada con Azure.
* **Criterios de Aceptación Técnicos Granulares (DoD):**
  - [ ] Configuración del servicio de notificaciones push (Firebase Cloud Messaging / Azure Notification Hubs) con credenciales seguras gestionadas vía variables de entorno en Azure Key Vault.
  - [ ] Plantilla de payload push configurada con canal de máxima prioridad (*high priority / sound: alarm / time-to-live: 0*), garantizando que suene incluso con modo "No Molestar" si los permisos del SO lo permiten.
  - [ ] Registro y actualización de tokens de dispositivos (`fcm_device_token`) asociado a cada usuario en la base de datos.
  - [ ] Cero secretos o llaves privadas expuestas en el repositorio Git.

#### `DAC05-194` — QA: flutter test + pytest E2E botón SOS
* **Capa:** QA | **Asignado:** Felipe Varas | **Estimación:** 3 pts
* **Descripción del Trabajo:** Ejecutar pruebas end-to-end del flujo de caída: detección → alerta → notificación push.
* **Criterios de Aceptación Técnicos Granulares (DoD):**
  - [ ] Prueba E2E backend: simulación de llamada HTTP a `/critical-event`, verificación de inserción en DB y comprobación de invocación al cliente FCM (mediante mock de transporte).
  - [ ] Prueba de integración frontend: simulación de recepción de mensaje `RemoteMessage` de Firebase y navegación por `go_router` hacia `ImmediateActionScreen`.
  - [ ] Cobertura de tests unitarios del handler de notificaciones y 100% de pruebas en verde en pipeline CI.

#### `DAC05-195` — PR: Peer review y merge a main - Botón SOS
* **Capa:** DoD / Git | **Asignado:** Franco Barra | **Estimación:** 1 pt
* **Descripción del Trabajo:** Crear Pull Request en GitHub hacia rama main, obtener aprobación de al menos un revisor técnico, realizar Squash and Merge una vez aprobado.
* **Criterios de Aceptación Técnicos Granulares (DoD):**
  - [ ] Branch: `feature/DAC05-18-flujo-critico-caidas`.
  - [ ] Commits bajo la norma: `DAC05-18: <descripción en español>`.
  - [ ] PR con video o GIF demostrativo de la recepción de alerta y apertura de la pantalla de acción inmediata.
  - [ ] Aprobación de *Peer Review* por `@FRANCO . BARRA BARRA` o `@f.varasc`.
  - [ ] Merge a `main` con estrategia Squash.

---

## 5. DAC05-19 — Botón de SOS (8 pts)

* **Épica Padre:** `DAC05-102` (Alertas críticas y SOS)
* **Responsable de Historia:** Franco Barra
* **Fórmula INVEST:** Como adulto mayor, quiero tener un botón de SOS grande, accesible y de voz primero en mi pantalla principal, para solicitar auxilio fácilmente ante cualquier emergencia y saber de inmediato que mi pedido de ayuda fue transmitido.
* **Criterios de Aceptación BDD (Negocio):**
  * *Dado que* el adulto mayor se encuentra en la pantalla principal accesible, *cuando* presiona el botón de SOS o pronuncia el comando de voz ("Ayuda" / "SOS"), *entonces* el botón inicia una cuenta regresiva audible de 3 segundos para prevenir falsos toques antes de enviar la señal.
  * *Dado que* se confirma el envío de la señal de SOS, *cuando* el servidor responde exitosamente, *entonces* la pantalla muestra una animación clara y un mensaje de voz que dice: "Tu mensaje de ayuda ha sido enviado a tu familia".
  * *Dado que* un familiar confirma la recepción de la alerta en su aplicación, *cuando* dicha confirmación llega por WebSocket o Push silencioso, *entonces* el adulto mayor ve en pantalla: "¡Tu familiar ya fue notificado y viene en camino!".

### 📋 Gestión de Subtareas Técnicas (Arquitectura Compartida con DAC05-18)
Esta historia comparte el motor backend, la infraestructura de mensajería push y la tubería de QA con `DAC05-18` (`DAC05-192` a `DAC05-195`). Las validaciones específicas para el adulto mayor contempladas en dichas subtareas son:

- [ ] **En Backend (`DAC05-192`):** Soporte explícito para `event_type = 'sos_manual'` con flag de confirmación bidireccional (`acknowledged_by_family: boolean`).
- [ ] **En Infraestructura Push (`DAC05-193`):** Canal push específico para retorno de confirmación (*receipt acknowledgement*) hacia la aplicación del adulto mayor.
- [ ] **En QA E2E (`DAC05-194`):** Escenario de prueba de estrés validando latencia de ida y vuelta (*round-trip latency*) inferior a 3 segundos entre pulsación del SOS y acuse de recibo.

---

## 6. DAC05-20 — Umbrales de alerta (5 pts)

* **Épica Padre:** `DAC05-102` (Alertas críticas y SOS)
* **Responsable de Historia:** Franco Barra
* **Fórmula INVEST:** Como familiar o médico, quiero configurar umbrales mínimos y máximos personalizados para los signos vitales del paciente, para que las alertas se disparen únicamente ante desviaciones clínicas relevantes.
* **Criterios de Aceptación BDD (Negocio):**
  * *Dado que* el familiar o médico accede a la configuración clínica del paciente, *cuando* ajusta los rangos seguros de Frecuencia Cardíaca (ej: 60 - 100 lpm) o SpO2 (ej: min 92%), *entonces* el sistema valida que el mínimo sea estrictamente menor que el máximo y guarda la configuración.
  * *Dado que* ingresa una nueva lectura de signos vitales, *cuando* el valor excede el umbral superior o cae bajo el inferior, *entonces* el motor de evaluación detona automáticamente una alerta con la severidad correspondiente.

### 📊 Tabla Resumen de Subtareas (Jira DAC05)

| Clave Jira | Título | Capa | Descripción | Asignado | Estimación |
|:---|:---|:---|:---|:---|:---|
| **DAC05-196** | UI: Pantalla configuración umbrales de signos vitales (Flutter) | Frontend | Crear pantalla para configurar umbrales mínimos y máximos por tipo de vital (FC, SpO2, temperatura) con validación de rango. | Franco Barra | 2 pts |
| **DAC05-197** | API: Endpoint CRUD umbrales de alerta (FastAPI) | Backend | Implementar endpoints CRUD para umbrales de vitales: crear, leer, actualizar, eliminar por paciente. | Franco Barra | 2 pts |
| **DAC05-198** | DB: Modelo y migración tabla alert_thresholds (PostgreSQL) | Base de Datos | Crear migración Alembic para tabla alert_thresholds con campos: tipo_vital, min_value, max_value, paciente_id, updated_by. | Franco Barra | 2 pts |
| **DAC05-199** | QA: flutter test + flutter analyze umbrales | QA | Ejecutar pruebas unitarias y de widget del módulo de umbrales. Verificar que flutter analyze no tenga advertencias. | Felipe Varas | 2 pts |
| **DAC05-200** | PR: Peer review y merge a main - Umbrales de alerta | DoD / Git | Crear Pull Request en GitHub hacia rama main, obtener aprobación de al menos un revisor técnico, realizar Squash and Merge una vez aprobado. | Franco Barra | 1 pt |

### 🔬 Especificación y Criterios de Aceptación Granulares por Subtarea

#### `DAC05-196` — UI: Pantalla configuración umbrales de signos vitales (Flutter)
* **Capa:** Frontend | **Asignado:** Franco Barra | **Estimación:** 2 pts
* **Descripción del Trabajo:** Crear pantalla para configurar umbrales mínimos y máximos por tipo de vital (FC, SpO2, temperatura) con validación de rango.
* **Criterios de Aceptación Técnicos Granulares (DoD):**
  - [ ] Pantalla de configuración con controles deslizantes (*RangeSliders*) y campos numéricos para los signos vitales estándar: Frecuencia Cardíaca (FC), Saturación de Oxígeno (SpO2), Presión Arterial Sistólica/Diastólica y Temperatura.
  - [ ] Validación visual en tiempo real: impide guardar si `min_value >= max_value` o si los valores están fuera de rangos biológicamente posibles (ej: FC < 30 o > 250).
  - [ ] Carga de valores por defecto clínicos estándar con botón "Restablecer a valores recomendados".
  - [ ] Mensajes de confirmación tipo SnackBar tras guardar cambios exitosamente y gestión de estado reactiva con Riverpod.
  - [ ] `flutter analyze` sin inconsistencias ni lints pendientes.

#### `DAC05-197` — API: Endpoint CRUD umbrales de alerta (FastAPI)
* **Capa:** Backend | **Asignado:** Franco Barra | **Estimación:** 2 pts
* **Descripción del Trabajo:** Implementar endpoints CRUD para umbrales de vitales: crear, leer, actualizar, eliminar por paciente.
* **Criterios de Aceptación Técnicos Granulares (DoD):**
  - [ ] Endpoints implementados:
    - `GET /api/v1/patients/{id}/thresholds`: Retorna la lista de umbrales activos del paciente.
    - `PUT /api/v1/patients/{id}/thresholds`: Actualización o creación idempotente (*upsert*) de umbrales por tipo de vital.
  - [ ] Esquemas Pydantic v2 con validadores `@field_validator` que garanticen coherencia matemática (`min_value < max_value`) y límites clínicos válidos.
  - [ ] Restricción de permisos: solo usuarios con rol `doctor` o `family_admin` tienen autorización para escribir umbrales; cuidadores y otros miembros tienen acceso de solo lectura.
  - [ ] Respuestas HTTP tipificadas: `200 OK`, `400 Bad Request` (con detalle del error de validación) y `403 Forbidden`.

#### `DAC05-198` — DB: Modelo y migración tabla alert_thresholds (PostgreSQL)
* **Capa:** Base de Datos | **Asignado:** Franco Barra | **Estimación:** 2 pts
* **Descripción del Trabajo:** Crear migración Alembic para tabla alert_thresholds con campos: tipo_vital, min_value, max_value, paciente_id, updated_by.
* **Criterios de Aceptación Técnicos Granulares (DoD):**
  - [ ] Migración Alembic para la creación de la tabla `alert_thresholds`.
  - [ ] Columnas: `id` (UUID, PK), `patient_id` (UUID, FK a `patients(id)`), `vital_type` (VARCHAR(50) NOT NULL), `min_warning` (NUMERIC(6,2)), `max_warning` (NUMERIC(6,2)), `min_critical` (NUMERIC(6,2)), `max_critical` (NUMERIC(6,2)), `updated_by` (UUID, FK a `users(id)`), `updated_at` (TIMESTAMPTZ DEFAULT now()).
  - [ ] Restricción UNIQUE en `(patient_id, vital_type)` para evitar duplicidad de configuración por paciente.
  - [ ] Reversibilidad probada en script de migración (`upgrade` / `downgrade`).

#### `DAC05-199` — QA: flutter test + flutter analyze umbrales
* **Capa:** QA | **Asignado:** Felipe Varas | **Estimación:** 2 pts
* **Descripción del Trabajo:** Ejecutar pruebas unitarias y de widget del módulo de umbrales. Verificar que flutter analyze no tenga advertencias.
* **Criterios de Aceptación Técnicos Granulares (DoD):**
  - [ ] Tests unitarios en Flutter validando la lógica de validación de formularios (rangos cruzados erróneos).
  - [ ] Pruebas unitarias en FastAPI (`pytest`) probando el validador Pydantic ante payloads con `min >= max`.
  - [ ] Prueba de integración de persistencia: verificar que tras un `PUT`, un posterior `GET` retorne los nuevos valores exactos.
  - [ ] Verificación de linter estricto en ambos repositorios sin advertencias.

#### `DAC05-200` — PR: Peer review y merge a main - Umbrales de alerta
* **Capa:** DoD / Git | **Asignado:** Franco Barra | **Estimación:** 1 pt
* **Descripción del Trabajo:** Crear Pull Request en GitHub hacia rama main, obtener aprobación de al menos un revisor técnico, realizar Squash and Merge una vez aprobado.
* **Criterios de Aceptación Técnicos Granulares (DoD):**
  - [ ] Rama de trabajo: `feature/DAC05-20-umbrales-alerta`.
  - [ ] Commits: `DAC05-20: <descripción en español>`.
  - [ ] PR con checklist DoD validado y evidencia de tests unitarios pasando al 100%.
  - [ ] Aprobación de *Peer Review* por `@FRANCO . BARRA BARRA` o `@ce.gacitua`.
  - [ ] Fusión mediante *Squash and Merge* hacia `main`.

---

## 7. DAC05-22 — Observaciones e incidentes (5 pts)

* **Épica Padre:** `DAC05-103` (Bitácora de cuidado)
* **Responsable de Historia:** Felipe Varas
* **Fórmula INVEST:** Como cuidadora, quiero registrar observaciones e incidentes del cuidado diario adjuntando notas y evidencia fotográfica, para mantener un expediente visual fidedigno que dé tranquilidad al familiar.
* **Criterios de Aceptación BDD (Negocio):**
  * *Dado que* la cuidadora detecta un incidente (ej: hematoma leve, desánimo, rechazo de comida), *cuando* completa el formulario y adjunta una fotografía desde la cámara o galería, *entonces* el sistema guarda la bitácora con timestamp y la imagen en almacenamiento seguro.
  * *Dado que* la cuidadora clasifica el incidente como `severo` o `urgente`, *cuando* presiona guardar, *entonces* el sistema notifica de inmediato al familiar vía push además de dejar el registro en la bitácora.
  * *Dado que* el familiar revisa la bitácora del día, *cuando* abre el registro, *entonces* puede visualizar la fotografía mediante una URL segura con vigencia temporal controlada.

### 📊 Tabla Resumen de Subtareas (Jira DAC05)

| Clave Jira | Título | Capa | Descripción | Asignado | Estimación |
|:---|:---|:---|:---|:---|:---|
| **DAC05-206** | UI: Formulario observaciones con foto (Flutter) | Frontend | Crear formulario para registrar observaciones e incidentes con adjunto de foto, bitácora de cuidado y clasificación de severidad. | Felipe Varas | 2 pts |
| **DAC05-207** | API: Endpoint POST observaciones e incidentes (FastAPI) | Backend | Implementar endpoint para crear observaciones con adjunto de foto, asociadas a paciente y cuidadora autenticada. | Felipe Varas | 3 pts |
| **DAC05-208** | Infra: Azure Blob Storage para fotos de observaciones | Infraestructura | Configurar Azure Blob Storage para almacenamiento seguro de fotos de observaciones con URLs firmadas SAS. | Franco Barra | 3 pts |
| **DAC05-209** | QA: flutter test + pytest observaciones | QA | Ejecutar pruebas frontend y backend del módulo de observaciones e incidentes con evidencia fotográfica. | Felipe Varas | 2 pts |
| **DAC05-210** | PR: Peer review y merge a main - Observaciones | DoD / Git | Crear Pull Request en GitHub hacia rama main, obtener aprobación de al menos un revisor técnico, realizar Squash and Merge una vez aprobado. | Felipe Varas | 1 pt |

### 🔬 Especificación y Criterios de Aceptación Granulares por Subtarea

#### `DAC05-206` — UI: Formulario observaciones con foto (Flutter)
* **Capa:** Frontend | **Asignado:** Felipe Varas | **Estimación:** 2 pts
* **Descripción del Trabajo:** Crear formulario para registrar observaciones e incidentes con adjunto de foto, bitácora de cuidado y clasificación de severidad.
* **Criterios de Aceptación Técnicos Granulares (DoD):**
  - [ ] Formulario con campos: selector de categoría (Alimentación, Estado de Ánimo, Lesión/Piel, Higiene, Otro), selector de severidad (Baja, Media, Alta), área de texto enriquecido para la descripción y componente de captura de imagen.
  - [ ] Integración con cámara y galería mediante `image_picker`, incluyendo compresión de imagen en el cliente antes de la subida para evitar consumo excesivo de datos móviles.
  - [ ] Vista previa interactiva de la imagen seleccionada con opción de eliminar o reemplazar antes de enviar.
  - [ ] Barra de progreso lineal visible durante la subida del archivo multimedia.
  - [ ] Manejo de Clean Architecture (`presentation/screens/observations/`) y `flutter analyze` limpio al 100%.

#### `DAC05-207` — API: Endpoint POST observaciones e incidentes (FastAPI)
* **Capa:** Backend | **Asignado:** Felipe Varas | **Estimación:** 3 pts
* **Descripción del Trabajo:** Implementar endpoint para crear observaciones con adjunto de foto, asociadas a paciente y cuidadora autenticada.
* **Criterios de Aceptación Técnicos Granulares (DoD):**
  - [ ] Endpoint `POST /api/v1/patients/{id}/observations` con soporte `multipart/form-data` (o flujo en dos pasos: generación de SAS token + POST de metadata).
  - [ ] Validación de archivos en el backend: solo se aceptan formatos de imagen seguros (`image/jpeg`, `image/png`, `image/webp`) con tamaño máximo de 5 MB.
  - [ ] Persistencia de la observación en la base de datos vinculando el `patient_id`, el `caregiver_id` (autenticado) y la URL del blob en Azure.
  - [ ] Endpoint `GET /api/v1/patients/{id}/observations` que retorne lista cronológica paginada, inyectando URLs firmadas SAS de lectura temporales en cada imagen.
  - [ ] Respuestas HTTP: `201 Created` con payload de la observación creada; `400 Bad Request` ante archivos inválidos; `403 Forbidden` si no tiene membresía.

#### `DAC05-208` — Infra: Azure Blob Storage para fotos de observaciones
* **Capa:** Infraestructura | **Asignado:** Franco Barra | **Estimación:** 3 pts
* **Descripción del Trabajo:** Configurar Azure Blob Storage para almacenamiento seguro de fotos de observaciones con URLs firmadas SAS.
* **Criterios de Aceptación Técnicos Granulares (DoD):**
  - [ ] Contenedor privado creado en Azure Blob Storage (ej: `care-observations`) sin acceso público anónimo habilitado.
  - [ ] Módulo backend para la generación de tokens Shared Access Signature (SAS) con política de acceso restringido (expiración de lectura máxima de 60 minutos).
  - [ ] Parámetros de conexión gestionados vía variables de entorno (`AZURE_STORAGE_CONNECTION_STRING` o credenciales administradas `DefaultAzureCredential`), sin credenciales en código.
  - [ ] Configuración CORS en el Storage Account para permitir visualización desde la aplicación Flutter Web y Móvil.

#### `DAC05-209` — QA: flutter test + pytest observaciones
* **Capa:** QA | **Asignado:** Felipe Varas | **Estimación:** 2 pts
* **Descripción del Trabajo:** Ejecutar pruebas frontend y backend del módulo de observaciones e incidentes con evidencia fotográfica.
* **Criterios de Aceptación Técnicos Granulares (DoD):**
  - [ ] Tests backend (`pytest`): validación de subida de archivos (mockeando el cliente de Azure Blob), prueba de rechazo ante archivos que superen 5MB o extensiones prohibidas (ej: `.exe`, `.pdf`).
  - [ ] Tests frontend (`flutter test`): validación del estado del formulario (botón guardar deshabilitado si no hay descripción o si la subida está en curso).
  - [ ] Verificación de análisis estático completo sin advertencias.

#### `DAC05-210` — PR: Peer review y merge a main - Observaciones
* **Capa:** DoD / Git | **Asignado:** Felipe Varas | **Estimación:** 1 pt
* **Descripción del Trabajo:** Crear Pull Request en GitHub hacia rama main, obtener aprobación de al menos un revisor técnico, realizar Squash and Merge una vez aprobado.
* **Criterios de Aceptación Técnicos Granulares (DoD):**
  - [ ] Rama de trabajo: `feature/DAC05-22-observaciones-incidentes-fotos`.
  - [ ] Commits: `DAC05-22: <descripción en español>`.
  - [ ] PR detallando la estrategia de almacenamiento seguro en Azure y captura de pantalla del formulario.
  - [ ] Aprobación de *Peer Review* por `@f.varasc` o `@FRANCO . BARRA BARRA`.
  - [ ] Fusión mediante *Squash and Merge* a `main`.

---

## 8. DAC05-24 — Notas de relevo de turno (5 pts)

* **Épica Padre:** `DAC05-103` (Bitácora de cuidado)
* **Responsable de Historia:** Felipe Varas
* **Fórmula INVEST:** Como cuidadora, quiero registrar una nota formal de relevo al concluir mi turno laboral, para que la colega entrante y la familia conozcan las novedades y tareas pendientes de forma clara y oportuna.
* **Criterios de Aceptación BDD (Negocio):**
  * *Dado que* la cuidadora finaliza su turno, *cuando* redacta su nota de relevo detallando pendientes y observaciones generales, *entonces* el sistema sella el turno anterior y guarda la nota en el expediente.
  * *Dado que* la siguiente cuidadora inicia su turno y realiza el check-in, *cuando* ingresa a la aplicación, *entonces* el sistema le presenta obligatoriamente la nota de relevo dejada por la colega anterior para su lectura y acuse de recibo.
  * *Dado que* el familiar revisa la aplicación, *cuando* consulta el módulo de bitácora, *entonces* visualiza el historial de relevos con autor, fecha y hora de entrega.

### 📊 Tabla Resumen de Subtareas (Jira DAC05)

| Clave Jira | Título | Capa | Descripción | Asignado | Estimación |
|:---|:---|:---|:---|:---|:---|
| **DAC05-216** | UI: Pantalla notas de relevo de turno (Flutter) | Frontend | Crear pantalla para dejar notas de relevo al finalizar turno, con observaciones y tareas pendientes, visibles para la siguiente cuidadora. | Felipe Varas | 2 pts |
| **DAC05-217** | API: Endpoint CRUD notas de relevo de turno (FastAPI) | Backend | Implementar endpoints CRUD para notas de relevo de turno: crear, leer, actualizar, eliminar por turno y paciente. | Felipe Varas | 2 pts |
| **DAC05-218** | DB: Migración tabla shift_handover_notes (PostgreSQL) | Base de Datos | Crear migración Alembic para tabla shift_handover_notes con campos: turno_id, paciente_id, cuidadora_id, observaciones, tareas_pendientes, fecha_creacion. | Felipe Varas | 2 pts |
| **DAC05-219** | QA: flutter test + flutter analyze relevo de turno | QA | Ejecutar pruebas unitarias y de widget del módulo de notas de relevo. Verificar que flutter analyze no tenga advertencias. | Felipe Varas | 2 pts |
| **DAC05-220** | PR: Peer review y merge a main - Notas de relevo | DoD / Git | Crear Pull Request en GitHub hacia rama main, obtener aprobación de al menos un revisor técnico, realizar Squash and Merge una vez aprobado. | Felipe Varas | 1 pt |

### 🔬 Especificación y Criterios de Aceptación Granulares por Subtarea

#### `DAC05-216` — UI: Pantalla notas de relevo de turno (Flutter)
* **Capa:** Frontend | **Asignado:** Felipe Varas | **Estimación:** 2 pts
* **Descripción del Trabajo:** Crear pantalla para dejar notas de relevo al finalizar turno, con observaciones y tareas pendientes, visibles para la siguiente cuidadora.
* **Criterios de Aceptación Técnicos Granulares (DoD):**
  - [ ] Pantalla para redacción de nota de fin de turno con campos estructurados: "Resumen de la Jornada", "Medicamentos Suministrados / Pendientes" y "Alertas Especiales para el Siguiente Turno".
  - [ ] Diálogo o pantalla modal de bienvenida para la cuidadora entrante que muestre la última nota de relevo con botón explícito "Entendido / Iniciar Turno".
  - [ ] Historial colapsable de notas de relevo anteriores para consulta retrospectiva por parte del familiar.
  - [ ] Integración con Riverpod y validación visual de campos obligatorios antes de permitir el envío.
  - [ ] `flutter analyze` sin observaciones.

#### `DAC05-217` — API: Endpoint CRUD notas de relevo de turno (FastAPI)
* **Capa:** Backend | **Asignado:** Felipe Varas | **Estimación:** 2 pts
* **Descripción del Trabajo:** Implementar endpoints CRUD para notas de relevo de turno: crear, leer, actualizar, eliminar por turno y paciente.
* **Criterios de Aceptación Técnicos Granulares (DoD):**
  - [ ] Endpoint `POST /api/v1/patients/{id}/shift-handovers` para registrar la nota de relevo asociada al `patient_id` y al `caregiver_id` autenticado.
  - [ ] Endpoint `GET /api/v1/patients/{id}/shift-handovers/latest` para obtener de forma eficiente la última nota registrada antes del inicio del nuevo turno.
  - [ ] Endpoint `GET /api/v1/patients/{id}/shift-handovers` con paginación para el historial del familiar.
  - [ ] Reglas de negocio: asocia automáticamente el `check_in_id` del turno activo y marca dicho turno como concluido (`check_out_at = now()`).
  - [ ] Respuestas estructuradas en Pydantic v2 con códigos `201 Created` y `200 OK`.

#### `DAC05-218` — DB: Migración tabla shift_handover_notes (PostgreSQL)
* **Capa:** Base de Datos | **Asignado:** Felipe Varas | **Estimación:** 2 pts
* **Descripción del Trabajo:** Crear migración Alembic para tabla shift_handover_notes con campos: turno_id, paciente_id, cuidadora_id, observaciones, tareas_pendientes, fecha_creacion.
* **Criterios de Aceptación Técnicos Granulares (DoD):**
  - [ ] Migración Alembic reversible para la tabla `shift_handover_notes`.
  - [ ] Estructura relacional: `id` (UUID, PK), `patient_id` (UUID, FK a `patients(id)`), `caregiver_id` (UUID, FK a `users(id)`), `checkin_id` (UUID, FK a `caregiver_checkins(id)` NULL), `summary` (TEXT NOT NULL), `pending_tasks` (TEXT), `special_instructions` (TEXT), `acknowledged_by` (UUID, FK a `users(id)` NULL), `acknowledged_at` (TIMESTAMPTZ NULL), `created_at` (TIMESTAMPTZ DEFAULT now()).
  - [ ] Índices en `(patient_id, created_at DESC)` y `(caregiver_id, created_at)`.
  - [ ] Pruebas locales de `upgrade` y `downgrade` sin pérdida de integridad de esquema.

#### `DAC05-219` — QA: flutter test + flutter analyze relevo de turno
* **Capa:** QA | **Asignado:** Felipe Varas | **Estimación:** 2 pts
* **Descripción del Trabajo:** Ejecutar pruebas unitarias y de widget del módulo de notas de relevo. Verificar que flutter analyze no tenga advertencias.
* **Criterios de Aceptación Técnicos Granulares (DoD):**
  - [ ] Tests de widget verificando el flujo de acuse de recibo de la nota de relevo por parte de la cuidadora entrante.
  - [ ] Pruebas unitarias backend validando el cierre del turno tras la emisión exitosa de la nota de relevo.
  - [ ] Cobertura de pruebas unitarias sobre controladores y repositorios superior al 80%.
  - [ ] `flutter analyze` y `ruff` ejecutados con 0 errores y 0 warnings.

#### `DAC05-220` — PR: Peer review y merge a main - Notas de relevo
* **Capa:** DoD / Git | **Asignado:** Felipe Varas | **Estimación:** 1 pt
* **Descripción del Trabajo:** Crear Pull Request en GitHub hacia rama main, obtener aprobación de al menos un revisor técnico, realizar Squash and Merge una vez aprobado.
* **Criterios de Aceptación Técnicos Granulares (DoD):**
  - [ ] Rama: `feature/DAC05-24-notas-relevo-turno`.
  - [ ] Commits bajo estándar: `DAC05-24: <descripción en español>`.
  - [ ] Pull Request con evidencia visual de la interfaz y descripción técnica del cierre de turno.
  - [ ] Aprobación de *Peer Review* por `@f.varasc` o `@cl.iosue`.
  - [ ] Fusión mediante *Squash and Merge* hacia `main`.

---

## 📊 Matriz Consolidada de Trazabilidad en Jira Software

| Historia | Puntos | Subtareas Verificadas en Jira | Capas Técnicas Abarcadas | Responsable |
|:---|:---:|:---|:---|:---|
| **DAC05-11** (Semáforo Bienestar) | 3 | `DAC05-177` a `DAC05-181` (5) | Frontend · Backend · DB · QA · DoD | César Gacitúa |
| **DAC05-21** (Check-in Cuidadora) | 5 | `DAC05-201` a `DAC05-205` (5) | Frontend · Backend · DB · QA · DoD | César Gacitúa |
| **DAC05-17** (Centro de Alertas) | 5 | `DAC05-187` a `DAC05-191` (5) | Frontend · Backend · DB · QA · DoD | Claudia Iosue |
| **DAC05-18** (Flujo Caídas) | 5 | `DAC05-84..86` + `DAC05-192..195` (7) | Frontend · Backend · Infra · QA · DoD | Franco Barra |
| **DAC05-19** (Botón SOS) | 8 | Compartidas con DAC05-18 (Motor común) | Accesibilidad · Push · Latencia | Franco Barra |
| **DAC05-20** (Umbrales Alerta) | 5 | `DAC05-196` a `DAC05-200` (5) | Frontend · Backend · DB · QA · DoD | Franco Barra |
| **DAC05-22** (Observaciones / Fotos) | 5 | `DAC05-206` a `DAC05-210` (5) | Frontend · Backend · Infra (Azure) · QA · DoD | Felipe Varas |
| **DAC05-24** (Notas de Relevo) | 5 | `DAC05-216` a `DAC05-220` (5) | Frontend · Backend · DB · QA · DoD | Felipe Varas |

**Totales del Sprint en Jira:** **7 Historias Activas** · **34 Subtareas Técnicas Sincronizadas** · **41 Puntos Fibonacci**
