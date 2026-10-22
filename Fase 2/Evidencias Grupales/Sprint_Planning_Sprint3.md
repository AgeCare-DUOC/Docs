# 📋 Sprint Planning — Sprint 3 (AgeCare)

> **Proyecto:** AgeCare — Suite de Cuidado de Personas Mayores  
> **Asignatura:** APT Capstone (Ingeniería en Informática — DUOC UC)  
> **Contraparte Empresarial:** Alloxentric / Wellq Co  
> **Fase:** 2 — Desarrollo Proyecto APT (Sprint 3)  
> **Sprint Jira:** SPRINT 3 "Bitácora y comunic." (ID 10, estado: future)  
> **Período:** 1 semana (timeboxed)  
> **Versión:** 1.1  
> **Fecha:** Octubre 2026  
> **Estado:** Revisado — Ajuste de alcance y carga de trabajo

---

## 1. Contexto y entrada del Sprint

### 1.1 Estado del Sprint 2

El Sprint 2 "Salud, medicamentos A" (ID 9) se cerró completamente:

| Métrica | Valor |
|---------|-------|
| Issues totales | 8 historias + 83 subtareas |
| Estado final | 100% Done (Finalizado) |
| Velocity Sprint 2 | 32 puntos Fibonacci |
| Asignación | César Gacitúa, Felipe Varas, Claudia Iosue, Franco Barra |
| Claves Jira | DAC05-3, 6, 10, 12, 14, 15, 16, 111 |

### 1.2 Sprint 3 

| Campo | Valor |
|-------|-------|
| Nombre | SPRINT 3 "Bitácora y comunic." |
| ID | 10 |
| Estado | future |
| Goal Jira | **"Que la cuidadora opere su jornada completa (check-in, observaciones, relevo) y que familiar/cuidadora puedan comunicarse por chat en tiempo real"** |
| Fecha inicio | 2026-10-17 |
| Fecha fin | 2026-10-23 |


---

## 2. Sprint Goal (Sprint 3)

> *"El equipo entrega la bitácora de cuidado y comunicación de cuidadoras (check-in, observaciones, relevo, chat), junto con alertas críticas (SOS, caídas, umbrales), todo con Vertical Slicing end-to-end y CI/CD refinado, manteniendo la trazabilidad DoD al 100%."*

**Alineación:** Cierra el núcleo de medicación (Sprint 2, alcance Must del proyecto) y lleva el sistema a un entorno real con notificaciones en tiempo real, alineado con la propuesta de valor de Alloxentric (paz mental al familiar) y con los entregables académicos RA2/RA3.

---

## 3. Distribución de responsabilidades (Sprint 3)

| Integrante | Responsabilidades principales | Issues asignados (Sprint 3) |
|------------|------------------------------|------------------------------|
| **César Gacitúa** | Sprint Plannings + CI/CD (refinar scripts de integración y despliegue) + Desarrollo | DAC05-11, 21 |
| **Franco Barra** | Sprint Reviews + Infra (Azure, GitHub, Vercel) + Desarrollo | DAC05-18, 19, 20 |
| **Felipe Varas** | Sprint Retrospectives + PPTs + QA | DAC05-22, 24 |
| **Claudia Iosue** | Meeting, Weeklys, Corestream, Documentación | DAC05-17 |

---

## 4. Historias de Usuario (User Stories) — Sprint Backlog

### 4.1 DAC05-11 — Pantalla de inicio con semáforo de bienestar

| Campo | Valor |
|-------|-------|
| **Título** | AGE-305 Pantalla de inicio con semáforo de bienestar del paciente |
| **Responsable** | César Gacitúa |
| **Puntos (Fibonacci)** | 3 |
| **Prioridad** | Medium |
| **Tipo** | Historia |
| **Parent** | DAC05-100 |

**Descripción (INVEST):**
> Como familiar, quiero ver un semáforo de bienestar en la pantalla de inicio que indique si mi adulto mayor se encuentra bien, para saber de un vistazo si requiere mi atención.

**Criterios de aceptación (BDD/Gherkin):**
```
Dado que el familiar ha iniciado sesión correctamente
Cuando accede a la pantalla de inicio
Entonces visualiza un semáforo con estado: verde (ok), amarillo (warning) o rojo (critical)

Dado que existen signos vitales registrados del paciente
Cuando el familiar consulta la pantalla de inicio
Entonces el semáforo refleja el estado más reciente de los vitales

Dado que no hay datos de vitales disponibles
Cuando el familiar abre la pantalla de inicio
Entonces el sistema muestra un estado "sin datos" y permite cargar vitales
```

**Subtareas (Vertical Slicing):**
| Subtarea | Clave | Capa | Responsable |
|----------|-------|------|-------------|
| UI: Pantalla semáforo bienestar (Flutter) | DAC05-226 | Frontend | César Gacitúa |
| API: Endpoint GET /api/v1/patients/{id}/wellbeing (FastAPI) | DAC05-227 | Backend | César Gacitúa |
| DB: Modelo y migración para lecturas de signos vitales (PostgreSQL) | DAC05-228 | Base de datos | César Gacitúa |
| QA: flutter test + flutter analyze semáforo bienestar | DAC05-229 | QA | Felipe Varas |
| PR: Peer review y merge a main - Semáforo bienestar | DAC05-230 | DoD / Git | César Gacitúa |

---

### 4.2 DAC05-21 — Check-in diario de la cuidadora

| Campo | Valor |
|-------|-------|
| **Título** | AGE-604 Check-in diario de la cuidadora con lista de tareas pendientes |
| **Responsable** | César Gacitúa |
| **Puntos (Fibonacci)** | 5 |
| **Prioridad** | Medium |
| **Tipo** | Historia |
| **Parent** | DAC05-103 |

**Descripción (INVEST):**
> Como cuidadora, quiero registrar mi check-in al inicio del turno y ver mi lista de tareas diarias, para llevar un control organizado del cuidado del adulto mayor.

**Criterios de aceptación (BDD/Gherkin):**
```
Dado que la cuidadora inicia su turno
Cuando presiona el botón de check-in
Entonces el sistema registra la entrada con fecha y hora

Dado que existe una lista de tareas diarias para el paciente
Cuando la cuidadora accede a su vista diaria
Entonces visualiza las tareas pendientes, completadas y omitidas del día

Dado que la cuidadora marca una tarea como completada
Cuando guarda el cambio
Entonces el sistema actualiza el estado y registra la hora de completado
```

**Subtareas:**
| Subtarea | Clave | Capa | Responsable |
|----------|-------|------|-------------|
| UI: Pantalla check-in y lista de tareas diarias (Flutter) | DAC05-231 | Frontend | César Gacitúa |
| API: Endpoint check-in y tareas diarias (FastAPI) | DAC05-232 | Backend | César Gacitúa |
| DB: Migración tablas check_in y daily_tasks (PostgreSQL) | DAC05-233 | Base de datos | César Gacitúa |
| QA: flutter test + flutter analyze check-in | DAC05-234 | QA | Felipe Varas |
| PR: Peer review y merge a main - Check-in diario | DAC05-235 | DoD / Git | César Gacitúa |

---

### 4.5 DAC05-17 — Centro de alertas

| Campo | Valor |
|-------|-------|
| **Título** | AGE-504 Centro de alertas: historial de notificaciones y canal de comunicación |
| **Responsable** | Claudia Iosue |
| **Puntos (Fibonacci)** | 5 |
| **Prioridad** | Lowest |
| **Tipo** | Historia |
| **Parent** | DAC05-102 |

**Descripción (INVEST):**
> Como familiar o cuidadora, quiero ver un centro de alertas con el historial de notificaciones y un canal de comunicación, para estar al tanto de eventos críticos y coordinar acciones.

**Criterios de aceptación (BDD/Gherkin):**
```
Dado que existen alertas generadas por el sistema
Cuando el usuario accede al centro de alertas
Entonces visualiza el historial cronológico de notificaciones con tipo y estado

Dado que hay una alerta crítica sin leer
Cuando el usuario abre el centro de alertas
Entonces la alerta se destaca visualmente y permite marcarla como leída

Dado que el usuario filtra las alertas por tipo
Cuando selecciona un tipo de alerta
Entonces el sistema muestra solo las alertas de ese tipo
```

**Subtareas:**
| Subtarea | Clave | Capa | Responsable |
|----------|-------|------|-------------|
| UI: Pantalla centro de alertas con historial (Flutter) | DAC05-236 | Frontend | Claudia Iosue |
| API: Endpoint GET alertas con historial (FastAPI) | DAC05-237 | Backend | Claudia Iosue |
| DB: Modelo y migración tabla alerts (PostgreSQL) | DAC05-238 | Base de datos | Claudia Iosue |
| QA: pytest + flutter analyze centro de alertas | DAC05-239 | QA | Felipe Varas |
| PR: Peer review y merge a main - Centro de alertas | DAC05-240 | DoD / Git | Claudia Iosue |

---

### 4.4 DAC05-18 — Flujo crítico ante caídas

| Campo | Valor |
|-------|-------|
| **Título** | AGE-505 Flujo crítico de atención inmediata ante detección de caída |
| **Responsable** | Franco Barra |
| **Puntos (Fibonacci)** | 5 |
| **Prioridad** | Lowest |
| **Tipo** | Historia |
| **Parent** | DAC05-102 |

**Descripción (INVEST):**
> Como cuidadora o familiar, quiero recibir una alerta inmediata cuando se detecte una caída del adulto mayor, para actuar rápidamente y verificar su estado.

**Criterios de aceptación (BDD/Gherkin):**
```
Dado que el wearable detecta un evento de caída
Cuando ocurre la detección
Entonces el sistema genera una alerta crítica de tipo "caída" y la envía en tiempo real

Dado que se genera una alerta de caída
Cuando el familiar o cuidadora la recibe
Entonces puede marcar la alerta como "atendida" o "falsa alarma"

Dado que hay una alerta de caída activa
Cuando pasa el tiempo de gracia sin confirmación
Entonces el sistema reenvía la notificación al contacto secundario
```

**Subtareas:**
| Subtarea | Clave | Capa | Responsable |
|----------|-------|------|-------------|
| UI: Pantalla de acción inmediata (existente) | DAC05-84 | Frontend | Franco Barra |
| Lógica de botones de llamada (existente) | DAC05-85 | Frontend | Franco Barra |
| Probar flujo alcanzable con app cerrada (existente) | DAC05-86 | QA | Franco Barra |
| API: Endpoint POST alertas SOS | DAC05-241 | Backend | Franco Barra |
| Infra: Notificación push SOS (FCM/APNs - Azure) | DAC05-242 | Infraestructura | Franco Barra |
| QA: flutter test + pytest E2E botón SOS | DAC05-243 | QA | Felipe Varas |
| PR: Peer review y merge a main - Botón SOS | DAC05-244 | DoD / Git | Franco Barra |

---

### 4.5 DAC05-19 — Botón de SOS

| Campo | Valor |
|-------|-------|
| **Título** | AGE-506 Botón de SOS de emergencia con confirmación de recepción |
| **Responsable** | Franco Barra |
| **Puntos (Fibonacci)** | 8 |
| **Prioridad** | Lowest |
| **Tipo** | Historia |
| **Parent** | DAC05-102 |

**Descripción (INVEST):**
> Como adulto mayor, quiero tener un botón de SOS accesible y de voz primero, para solicitar ayuda de emergencia y saber que mi solicitud fue recibida.

**Criterios de aceptación (BDD/Gherkin):**
```
Dado que el adulto mayor presiona el botón de SOS
Cuando se activa el botón
Entonces el sistema envía una alerta de emergencia a los contactos designados

Dado que se envía una alerta de SOS
Cuando un familiar la recibe y confirma
Entonces el adulto mayor ve una confirmación de "Solicitud recibida"

Dado que el botón de SOS está en la pantalla principal del adulto mayor
Cuando el adulto mayor lo ubica
Entonces el botón es de gran tamaño, con etiqueta de voz y color rojo distintivo
```

**Subtareas:** (compartidas con DAC05-18: DAC05-241 a 244)

---

### 4.6 DAC05-20 — Umbrales de alerta

| Campo | Valor |
|-------|-------|
| **Título** | AGE-507 Configuración de umbrales personalizados de alerta de signos vitales |
| **Responsable** | Franco Barra |
| **Puntos (Fibonacci)** | 5 |
| **Prioridad** | Lowest |
| **Tipo** | Historia |
| **Parent** | DAC05-102 |

**Descripción (INVEST):**
> Como familiar o médico, quiero configurar umbrales personalizados para cada signo vital, para recibir alertas solo cuando los valores estén fuera de rango seguro.

**Criterios de aceptación (BDD/Gherkin):**
```
Dado que soy familiar o médico autenticado
Cuando configuro un umbral mínimo y máximo para un signo vital (FC, SpO2, temperatura)
Entonces el sistema guarda la configuración y la aplica a futuras lecturas

Dado que existe un umbral configurado para SpO2
Cuando llega una lectura con valor por debajo del umbral mínimo
Entonces el sistema genera una alerta de tipo "SpO2 bajo"

Dado que el usuario modifica un umbral existente
Cuando guarda los cambios
Entonces el sistema aplica el nuevo umbral a lecturas posteriores
```

**Subtareas:**
| Subtarea | Clave | Capa | Responsable |
|----------|-------|------|-------------|
| UI: Pantalla configuración umbrales de signos vitales (Flutter) | DAC05-245 | Frontend | Franco Barra |
| API: Endpoint CRUD umbrales de alerta (FastAPI) | DAC05-246 | Backend | Franco Barra |
| DB: Modelo y migración tabla alert_thresholds (PostgreSQL) | DAC05-247 | Base de datos | Franco Barra |
| QA: flutter test + flutter analyze umbrales | DAC05-248 | QA | Felipe Varas |
| PR: Peer review y merge a main - Umbrales de alerta | DAC05-249 | DoD / Git | Franco Barra |

---

### 4.7 DAC05-22 — Observaciones e incidentes

| Campo | Valor |
|-------|-------|
| **Título** | AGE-605 Registro de observaciones e incidentes del cuidado con evidencia fotográfica |
| **Responsable** | Felipe Varas |
| **Puntos (Fibonacci)** | 5 |
| **Prioridad** | Medium |
| **Tipo** | Historia |
| **Parent** | DAC05-103 |

**Descripción (INVEST):**
> Como cuidadora, quiero registrar observaciones e incidentes con evidencia (fotos, notas), para documentar el estado del adulto mayor y compartirlo con el familiar.

**Criterios de aceptación (BDD/Gherkin):**
```
Dado que la cuidadora está en el registro de observaciones
Cuando describe un incidente y adjunta una foto como evidencia
Entonces el sistema guarda la observación con timestamp y la imagen asociada

Dado que existe una observación registrada
Cuando el familiar consulta el historial
Entonces visualiza la observación con su evidencia y fecha

Dado que la cuidadora clasifica un incidente como crítico
Cuando guarda el registro
Entonces el sistema genera una notificación al familiar inmediatamente
```

**Subtareas:**
| Subtarea | Clave | Capa | Responsable |
|----------|-------|------|-------------|
| UI: Formulario observaciones con foto (Flutter) | DAC05-250 | Frontend | Felipe Varas |
| API: Endpoint POST observaciones e incidentes (FastAPI) | DAC05-251 | Backend | Felipe Varas |
| Infra: Azure Blob Storage para fotos de observaciones | DAC05-252 | Infraestructura | Franco Barra |
| QA: flutter test + pytest observaciones | DAC05-253 | QA | Felipe Varas |
| PR: Peer review y merge a main - Observaciones | DAC05-254 | DoD / Git | Felipe Varas |

---

### 4.8 DAC05-24 — Notas de relevo de turno

| Campo | Valor |
|-------|-------|
| **Título** | AGE-607 Registro de notas de relevo de turno entre cuidadoras |
| **Responsable** | Felipe Varas |
| **Puntos (Fibonacci)** | 5 |
| **Prioridad** | Medium |
| **Tipo** | Historia |
| **Parent** | DAC05-103 |

**Descripción (INVEST):**
> Como cuidadora, quiero dejar notas de relevo al terminar mi turno, para que la próxima cuidadora tenga contexto del estado del adulto mayor y las tareas pendientes.

**Criterios de aceptación (BDD/Gherkin):**
```
Dado que la cuidadora está finalizando su turno
Cuando escribe una nota de relevo con observaciones y tareas pendientes
Entonces el sistema guarda la nota asociada al turno y al paciente

Dado que existe una nota de relevo del turno anterior
Cuando la siguiente cuidadora inicia su turno
Entonces visualiza la nota de relevo antes de comenzar sus tareas

Dado que el familiar consulta el historial de turnos
Cuando accede al expediente del paciente
Entonces visualiza las notas de relevo de cada cuidadora con fecha y hora
```

**Subtareas:**
| Subtarea | Clave | Capa | Responsable |
|----------|-------|------|-------------|
| UI: Pantalla notas de relevo de turno (Flutter) | DAC05-255 | Frontend | Felipe Varas |
| API: Endpoint CRUD notas de relevo de turno (FastAPI) | DAC05-256 | Backend | Felipe Varas |
| DB: Migración tabla shift_handover_notes (PostgreSQL) | DAC05-257 | Base de datos | Felipe Varas |
| QA: flutter test + flutter analyze relevo de turno | DAC05-258 | QA | Felipe Varas |
| PR: Peer review y merge a main - Notas de relevo | DAC05-259 | DoD / Git | Felipe Varas |

---

## 5. Resumen de puntos y capacidad

| Responsable | Issues | Puntos |
|-------------|--------|--------|
| César Gacitúa | DAC05-11, 21 | 3 + 5 = **8** |
| Franco Barra | DAC05-18, 19, 20 | 5 + 8 + 5 = **18** |
| Felipe Varas | DAC05-22, 24 | 5 + 5 = **10** |
| Claudia Iosue | DAC05-17 | 5 = **5** |
| **Total Sprint 3** | **7 User Stories** | **41 puntos Fibonacci** |

**Velocidad referencia Sprint 2:** 32 puntos  
**Compromiso Sprint 3:** 41 puntos (ajustado según capacidad real del equipo, ~25% por encima de velocity para permitir crecimiento sin sobrecarga)

---

## 6. Definición de Listo (DoR)

Ninguna historia ingresa al Sprint Backlog sin cumplir:

- [ ] **INVEST:** Independiente, Negociable, Valiosa, Estimable, Pequeña, Comprobable
- [ ] **Origen trazable:** Requerimiento de Alloxentric o entregable DUOC UC
- [ ] **Criterios de aceptación BDD:** 2-4 escenarios Gherkin (*Dado que... Cuando... Entonces...*)
- [ ] **Dependencias resueltas:** Modelos, contratos de API o diseños definidos
- [ ] **Estimación Fibonacci consensuada:** ≤ 8 puntos (si es más, descomponer)

---

## 7. Definición de Hecho (DoD)

Una historia no se considera Done sin cumplir el 100%:

- [ ] **Criterios de aceptación BDD verificados empíricamente**
- [ ] **Frontend (Flutter):** Clean Architecture, `flutter analyze` sin advertencias, responsive
- [ ] **Backend (FastAPI):** Endpoints async, Pydantic v2, manejo de errores HTTP, Swagger/OpenAPI actualizado
- [ ] **Infraestructura (Azure):** Bicep actualizado, sin secretos hardcodeados, Key Vault
- [ ] **Trazabilidad Git/Jira:**
  - Rama `feature/<CLAVE>-descripcion`
  - Commits `<CLAVE>: descripción en español`
  - PR aprobado por peer review y mergeado a `main`
  - Comentarios en Jira con menciones: `@cl.iosue`, `@FRANCO . BARRA BARRA`, `@f.varasc`, `@ce.gacitua`
- [ ] **QA:** `flutter test` / `pytest` al 100% verde
- [ ] **Evidencia académica:** Documentación conforme a pauta DUOC UC (RA1-RA3)

---

## 8. Trazabilidad Git-Jira

| Estándar | Convención |
|----------|------------|
| Clave de incidencia | `DAC05-XX`, `AGE-XX`, `SCRUM-XX` (inmutables) |
| Rama | `feature/<CLAVE>-descripcion-corta` |
| Commit | `<CLAVE>: descripción corta en español` |
| PR | Título con `[DAC05-XXX]`, Squash and Merge a `main` |
| Comentarios Jira | Menciones explícitas al equipo |
| Transiciones | Webhook automático: branch → In Progress, PR → In Review, merge → Done |

---

## 9. Métricas de control ágil

| Métrica | Objetivo | Herramienta |
|---------|----------|-------------|
| Velocity | ≥ 32 puntos (mínimo igualar Sprint 2) | Jira Velocity Chart |
| Burndown | Descenso lineal a cero al final del Sprint | Jira Board |
| Cycle Time | Tiempo In Progress → Done por historia | Jira / GitHub |
| Tasa de DoD | 100% de historias Done cumplen checklist | Auditoría SM en Daily |
| CFD | Inspección de cuellos de botella | Jira |

---

## 10. Riesgos y mitigaciones

| Riesgo | Impacto | Mitigación |
|--------|---------|------------|
| Scope creep (solicitudes Alloxentric fuera del goal) | Alto | Registrar en Product Backlog para Sprint 4 |
| César sobrecargado (3 roles) | Medio | Delegar tareas técnicas a Felipe y Franco desde el día 1 |
| WebSocket no funcional | Medio | Probar con endpoint de prueba antes de integrar al frontend |
| Sobreestimación de puntos (impacto en velocity) | Medio | Recalibrar compromisos en la reunión de Planning |

---

## 11. Alineación con Resultados de Aprendizaje (RA) DUOC UC

| RA | Descripción | Evidencia Sprint 3 |
|----|-------------|-------------------|
| RA1 | Diseña una propuesta de proyecto con competencias de egreso | Historias alineadas con negocio Alloxentric y Ley 21.805 |
| RA2 | Desarrolla el Proyecto APT según estándares de calidad | DoR/DoD, pruebas 100% verde, arquitectura limpia, IaC Bicep |
| RA3 | Presenta el Proyecto APT con evidencias de competencias | Este documento, registros de uso IA, sprint reports |

---

## 12. Compromisos para Sprint 3

| Compromiso | Responsable | Fecha límite |
|------------|-------------|--------------|
| Validar DoR/DoD en las 7 historias antes del Planning | César Gacitúa | Inicio Sprint 3 |
| Despliegue en Azure Container Apps validado | César Gacitúa | Fin Sprint 3 |
| Notificación push SOS (FCM/APNs) | Franco Barra | Fin Sprint 3 |
| Documentación OpenAPI completa | Claudia Iosue | Medio Sprint 3 |
| Delegación de tareas backend desde SM role | César Gacitúa | Inicio Sprint 3 |


---

## 13. Notas y cambios vs. versión anterior

| Cambio | Detalle |
|--------|---------|
| Puntos totales | Reducido de 57 a 41 puntos (ajuste a velocity real de 32) |
| DAC05-23 (Documentos) | Movido a Sprint 4 (no es core MVP) |
| DAC05-25 (Chat WebSocket) | Movido a Sprint 4 (complejo, puede esperar) |
| DAC05-13 (Medicamentos OCR) | Movido a Sprint 4 (redundante con trabajo Sprint 2) |
| César Gacitúa | Reducido de 32 a 8 puntos (delegación a Franco y Felipe) |
| DAC05-11 Padre | Corregido: DAC05-100 (Vitals, wearable y semáforo) |
| Claves de subtarea | Usadas claves nuevas (DAC05-226 a 259), sin reutilizar DAC05-84/85/86 |

