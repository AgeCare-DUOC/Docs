# 📋 Plan de Realineamiento y Priorización — 4 Semanas Restantes

**Proyecto:** AgeCare — Suite de Cuidado de Personas Mayores  
**Asignatura:** APT Capstone (Ingeniería en Informática — DUOC UC)  
**Contraparte Empresarial:** Alloxentric / Wellq Co  
**Autor:** César Gacitúa (Agent Orchestration & Scrum Master)  
**Fecha:** 29 de octubre de 2026  
**Versión:** 1.0  
**Estado:** Borrador para revisión y ejecución  
**Ubicación:** Documentos del Equipo / Plan de Realineamiento y Priorización — 4 Semanas Restantes.md

---

## 1. Contexto y Justificación

Tras la separación del equipo original, el proyecto continúa de forma individual con autonomía total (1 humano + 3 agentes especializados: Backend, Frontend, QA/DevOps). Quedan aproximadamente **4 semanas de clases** antes de la entrega final. Los sprints previos ya se cerraron, por lo que no es posible reabrir el pasado; hay que completar lo pendiente en el presente y priorizar lo que falta.

El diagnóstico de código fuente (Fase 0) reveló que el backend y frontend están **muy avanzados** respecto a lo que reflejaban los issues de Jira. El núcleo de salud (vitals, semáforo de bienestar, pantalla Salud) ya está implementado en ambos repositorios. Las brechas críticas son de integración y navegación, no de desarrollo desde cero.

Este documento es el **documento maestro** que guía las próximas 4 semanas. Incorpora:

- La **pirámide de valor** del Plan de Reorganización del Product Backlog (Sprint 2)
- La **matriz MoSCoW** ajustada a 4 semanas
- El **plan semanal** detallado (Semana 1-4)
- La **Definición de Listo (DoR)** y **Definición de Hecho (DoD)** de Sprint_Planning_Sprint3.md
- Las **convenciones Git-Jira** reutilizadas
- El **plan de diagnóstico de código** (Fase 0)

---

## 2. Pirámide de Valor para el Usuario Final

Basado en el `Plan de Reorganización del Product Backlog — Sprint 2.md` y la documentación de Alloxentric (Objetivos Generales y Específicos, Funcionalidades v1, Plan de Desarrollo v1).

### 2.1 Propuesta de Valor de Negocio

> *"Brindar paz mental y tranquilidad al familiar responsable que cuida a un adulto mayor a distancia, permitiéndole saber de un vistazo que su ser querido está bien."*

Marco regulatorio: Ley 21.805 (*Chile Cuida*), reconociendo el cuidado como un derecho social y facilitando la teleasistencia de adultos mayores dependientes.

### 2.2 Clasificación de Features por Tier (Pirámide de Valor)

| Tier | Característica | Justificación de Negocio | Impacto en "Paz Mental" | Prioridad MoSCoW |
|------|---------------|-------------------------|------------------------|------------------|
| 🔴 1 | **Autenticación real E2E** | Sin login funcional no hay app | Requisito base | Must |
| 🔴 1 | **Crear/gestionar perfil de paciente E2E** | Sin paciente no hay a quién monitorear | Requisito base | Must |
| 🔴 1 | **Monitoreo de signos vitales (semáforo)** | *"saber de un vistazo que su ser querido está bien"* | ⭐⭐⭐⭐⭐ | Must |
| 🔴 1 | **Gestión de medicamentos y adherencia** | 38.3% adultos mayores en dependencia funcional | ⭐⭐⭐⭐⭐ | Must |
| 🔴 1 | **Alertas críticas (caída, vital fuera de rango, medicamento no tomado)** | *"Las alertas son el principal valor para el familiar"* | ⭐⭐⭐⭐⭐ | Must |
| 🟡 2 | Invitación al círculo de cuidado E2E | Habilita modelo multi-rol | ⭐⭐⭐⭐ | Should |
| 🟡 2 | Check-in y bitácora de la cuidadora | Operación diaria del cuidado | ⭐⭐⭐⭐ | Should |
| 🟡 2 | SOS / Emergencia | Seguridad crítica pero de baja frecuencia | ⭐⭐⭐⭐ | Should |
| 🟢 3 | Chat de coordinación | Comunicación entre roles | ⭐⭐⭐ | Could |
| 🟢 3 | Asistente IA | Diferenciador tecnológico | ⭐⭐⭐ | Could |
| 🟢 3 | Vista adulto mayor accesible | Inclusión, voz primero | ⭐⭐⭐ | Could |
| ⚪ 4 | Marketplace, Premium, Entretenimiento | Monetización y engagement | ⭐⭐ | Won't (esta fase) |

### 2.3 Regla Inmutable

**El adulto mayor NUNCA paga ni debe enfrentar barreras de autenticación complejas.** (Modelo Freemium de Alloxentric)

---

## 3. Matriz MoSCoW Ajustada a 4 Semanas

Dado el tiempo limitado (4 sprints de 1 semana cada uno) y el trabajo individual con 3 agentes, se aplica MoSCoW estrictamente:

| Prioridad | Contenido | Semana Sugerida | Razón |
|-----------|-----------|-----------------|-------|
| **Must** | Vitals + semáforo + pantalla Salud (núcleo de salud) | Semana 1 (Sprint 3) | Es el objetivo original del Sprint 3 según Alloxentric y lo que el familiar espera ver primero |
| **Must** | Check-in cuidadora + tareas diarias | Semana 2 (Sprint 4) | Operación diaria de la cuidadora, valor inmediato para el familiar |
| **Must** | Observaciones e incidentes con foto | Semana 2 (Sprint 4) | Bitácora de cuidado, evidencia visual para el familiar |
| **Should** | Umbrales de alerta + centro de alertas | Semana 3 (Sprint 5) | Alerta temprana, pero depende de vitals (Semana 1) |
| **Should** | Botón SOS + flujo de caída | Semana 3 (Sprint 5) | Emergencia, crítico pero complejo; depende de push notifications |
| **Could** | Chat en tiempo real (WebSocket) | Semana 4 (Sprint 6) | Comunicación, valor alto pero técnicamente complejo |
| **Could** | Documentos del expediente (SAS) | Semana 4 (Sprint 6) | Repositorio médico, importante pero no bloqueante |
| **Could** | Vista del adulto mayor (voz primero) | Semana 4+ | Accesibilidad, diferencial de producto |
| **Won't** | Marketplace, Premium, Entretenimiento | Post-entrega | Monetización, no MVP académico |

---

## 4. Plan Semanal Detallado (4 Semanas)

### Semana 1 — Sprint 3: Núcleo de Salud (Vitals + Semáforo + Pantalla Salud)

**Objetivo:** Entregar lo que Alloxentric espera para el Sprint 3 según su roadmap (Plan de Desarrollo v1): datos de vitals fluyendo, semáforo de bienestar, pantalla de Salud con tendencias.

**Sprint Goal:** *"El equipo entrega la ingesta de signos vitales (wearable simulado + captura manual), el cálculo del semáforo de bienestar y la pantalla de Salud con tendencias, todo con Vertical Slicing end-to-end y CI/CD refinado, alineado con el roadmap de Alloxentric Sprint 3 y los entregables académicos RA2/RA3."*

| Día | Acción | Responsable | Entregable |
|-----|--------|-------------|------------|
| Lunes | Fase 0: Diagnóstico de código fuente (Backend + Frontend) | Tú + Agentes | `diagnostico-codigo.md` |
| Martes | Crear issues en Jira (10 historias + 19 subtareas) | Tú | Issues DAC05-222 a DAC05-250 en Sprint 3 |
| Miércoles | Implementar API ingesta de vitals + series + semáforo | Agent 1 (Backend) | Endpoints funcionando, tests verdes |
| Jueves | Implementar pantalla Salud + corregir ruta /health + useMocks | Agent 2 (Frontend) | UI conectada a API real, navegación funcional |
| Viernes | QA, pruebas, Bicep, PRs, merge a main | Agent 3 (QA/DevOps) | DoD al 100%, todo en main |

**Issues Jira creados:**
- DAC05-222 a DAC05-231 (10 historias de usuario)
- DAC05-232 a DAC05-250 (19 subtareas con Vertical Slicing)

**Puntos comprometidos:** ~31 Fibonacci (dentro del velocity de referencia de 32)

---

### Semana 2 — Sprint 4: Operación de la Cuidadora (Check-in + Tareas + Observaciones)

**Objetivo:** La cuidadora opera su jornada completa: check-in, lista de tareas, registro de observaciones con foto.

**Sprint Goal:** *"La cuidadora puede registrar su check-in, gestionar sus tareas diarias y documentar observaciones e incidentes con evidencia fotográfica, todo con trazabilidad end-to-end."*

| Día | Acción | Responsable | Entregable |
|-----|--------|-------------|------------|
| Lunes | Planning Sprint 4 | Tú | Sprint Goal definido, issues movidos de backlog |
| Martes–Miércoles | API check-in, daily_tasks, observaciones | Agent 1 (Backend) | Endpoints POST/GET, migraciones, tests |
| Jueves | UI check-in, tareas, formulario observaciones con foto | Agent 2 (Frontend) | Pantallas Flutter conectadas a API real |
| Viernes | Azure Blob Storage para fotos, QA, PRs, merge | Agent 3 + Agent 1 | SAS URLs, tests verdes, DoD al 100% |

**Issues Jira:** DAC05-21 (Check-in), DAC05-22 (Observaciones), subtareas asociadas

**Puntos:** ~15–18 Fibonacci

---

### Semana 3 — Sprint 5: Alertas, Push y SOS (Pilar Central)

**Objetivo:** Sistema de alertas en tiempo real, centro de alertas, umbrales configurables, botón SOS, flujo de caída.

**Sprint Goal:** *"El sistema genera alertas críticas en tiempo real (caída, vital fuera de rango, SOS), con notificaciones push y centro de alertas, permitiendo al familiar actuar inmediatamente ante emergencias."*

| Día | Acción | Responsable | Entregable |
|-----|--------|-------------|------------|
| Lunes | Planning Sprint 5 | Tú | Sprint Goal definido |
| Martes–Miércoles | Motor de alertas, endpoint SOS, umbrales | Agent 1 (Backend) | Endpoints críticos, lógica de alerta, tests |
| Jueves | Centro de alertas UI, push notifications, botón SOS UI | Agent 2 (Frontend) | Pantallas de alertas, notificaciones push |
| Viernes | Azure Notification Hubs/FCM, QA E2E, PRs, merge | Agent 3 (QA/DevOps) | Push funcionando, tests E2E, DoD al 100% |

**Issues Jira:** DAC05-17 (Centro de alertas), DAC05-18 (Flujo caídas), DAC05-19 (Botón SOS), DAC05-20 (Umbrales)

**Puntos:** ~20–23 Fibonacci (ajustar si excede velocity)

---

### Semana 4 — Sprint 6: Bitácora, Documentos + Estabilización + Demo Final

**Objetivo:** Notas de relevo de turno, documentos del expediente médico, regresión completa de sprints 1–5, preparación para demo final.

**Sprint Goal:** *"El sistema entrega notas de relevo entre turnos, documentos médicos con URLs firmadas SAS, y una versión estable y demostrable de todo el núcleo de salud, lista para la evaluación académica RA3."*

| Día | Acción | Responsable | Entregable |
|-----|--------|-------------|------------|
| Lunes | Planning Sprint 6 | Tú | Sprint Goal definido |
| Martes–Miércoles | Notas de relevo, documentos SAS, regresión completa | Agent 1 + Agent 2 | Endpoints, UI, pruebas de regresión |
| Jueves | Ajustes finales, pulido de UI, documentación académica | Tú + Agentes | Demo lista, informes RA1-RA3 |
| Viernes | Demo final, cierre de sprint, informe académico | Tú | Evidencia de competencias, sprint report |

**Issues Jira:** DAC05-24 (Notas de relevo), DAC05-23 (Documentos, si hay tiempo), regresión de sprints 1–5

**Puntos:** ~12–15 Fibonacci (dejar margen para imprevistos)

---

## 5. Definición de Listo (DoR)

*Reutilizada de Sprint_Planning_Sprint3.md (§6) y reglas-scrum-agecare.md (§1)*

Ninguna historia de usuario o ítem del backlog puede ser admitido en el **Sprint Backlog** durante el *Sprint Planning* sin cumplir de forma estricta los siguientes 5 requisitos:

| Requisito | Descripción |
|-----------|-------------|
| **1. INVEST** | Independiente, Negociable, Valiosa, Estimable, Pequeña (*Small*) y Comprobable (*Testable*). Reducir acoplamientos entre historias. |
| **2. Origen Trazable** | Fundamentada en un requerimiento de negocio de Alloxentric (`Documentos de la Empresa (Alloxentric)/`) o en un entregable/competencia académica de DUOC UC (`Documentos Academicos/`). |
| **3. Criterios de Aceptación BDD (Gherkin)** | Contiene entre 2 y 4 escenarios de prueba comprobables y no ambiguos redactados en formato Gherkin (*Dado que... Cuando... Entonces...*). |
| **4. Dependencias Resueltas** | Modelos de datos, contratos de endpoints de FastAPI o diseños/wireframes de Flutter requeridos están definidos o planificados dentro de la misma iteración. |
| **5. Estimación Consensuada** | El equipo ha asignado puntos de historia utilizando la escala Fibonacci consensuada (`1, 2, 3, 5, 8, 13`). Historias mayores a 8 puntos deben descomponerse previamente. |

---

## 6. Definición de Hecho (DoD)

*Reutilizada de Sprint_Planning_Sprint3.md (§7) y reglas-scrum-agecare.md (§2)*

Un incremento de software o entrega del Sprint solo se considera finalizado cuando cumple transversalmente con todos los criterios de la siguiente lista de verificación:

| Área | Criterio |
|------|----------|
| **Criterios de Aceptación** | Todos los escenarios BDD/Gherkin de la historia han sido verificados y aprobados empíricamente. |
| **Frontend (Flutter)** | Código organizado en Clean Architecture (`domain/data/application/presentation`), sin advertencias ni errores en `flutter analyze`, adaptable (responsive) y probado en Flutter Web/Móvil. |
| **Backend (FastAPI)** | Controladores asíncronos (`asyncpg`), esquemas Pydantic v2 con validación rígida, manejo estandarizado de errores HTTP, documentación Swagger/OpenAPI actualizada. |
| **Infraestructura Cloud (Azure)** | Plantillas Bicep actualizadas en `infra/azure/`, variables de entorno consumidas mediante `pydantic-settings`/`AppConfig` sin credenciales ni secretos *hardcodeados*, e integración con Azure Container Apps / PostgreSQL Flexible Server verificada. |
| **Trazabilidad Git / Jira** | Rama nombrada como `feature/<CLAVE>-descripcion` (usando la clave de Jira: `DAC05-XX`, `AGE-XX`, `SCRUM-XX`). Commits atómicos con formato `<CLAVE>: <descripción corta en español>`. Comentarios de avance en Jira incluyendo menciones al equipo (`@ce.gacitua`). Pull Request aprobado por revisión por pares (*Peer Review*) y fusionado en la rama base (`main`). |
| **QA** | Suite de pruebas unitarias/integración al 100% en verde (`flutter test` / `pytest`). |
| **Evidencia Académica (APT Capstone)** | Documentación técnica conforme a la pauta de evaluación de DUOC UC (RA1–RA3). |

---

## 7. Convenciones Git-Jira

*Reutilizada de Sprint_Planning_Sprint3.md (§8) y reglas-scrum-agecare.md*

| Estándar | Convención |
|----------|------------|
| **Clave de incidencia** | `DAC05-XX`, `AGE-XX`, `SCRUM-XX` (inmutables) |
| **Rama** | `feature/<CLAVE>-descripcion-corta` |
| **Commit** | `<CLAVE>: descripción corta en español` |
| **PR** | Título con `[DAC05-XXX]`, Squash and Merge a `main` |
| **Comentarios Jira** | Menciones explícitas al equipo (`@ce.gacitua`) |
| **Transiciones** | Webhook automático: branch → In Progress, PR → In Review, merge → Done |

### Flujo de Ramas (Merge antes de iniciar nuevas ramas)

1. Antes de crear cualquier rama nueva, actualizar `main`: `git checkout main && git pull origin main`
2. Crear la nueva rama desde `main` actualizado: `git checkout -b feature/<CLAVE>-descripcion`
3. Al completar una feature, hacer merge a `main`: `git checkout main && git merge --no-ff feature/<CLAVE>-feature-completada`
4. Eliminar la rama local y publicar: `git branch -d feature/<CLAVE>-feature-completada && git push origin main`
5. Las ramas de features independientes solo pueden crearse en paralelo si `main` está actualizado.

---

## 8. Plan de Diagnóstico de Código (Fase 0)

*Ejecutado el 29 de octubre de 2026. Resultado documentado en este plan.*

### 8.1 Backend-API (`Github/Backend-API`)

| Área | Qué se validó | Resultado |
|------|--------------|-----------|
| Estructura del repositorio | `app/`, `alembic/`, `tests/`, `infra/azure/`, `docker-compose.yml`, `Dockerfile` | ✅ Completa |
| Endpoints implementados | ~75 endpoints REST + 1 WebSocket (`/ws/chat/{patient_id}`) | ✅ Todos los del núcleo de salud implementados |
| Modelos de BD y migraciones | 40 tablas en SQLAlchemy + 2 migraciones Alembic | ✅ Todas las tablas necesarias existen |
| Pruebas (pytest) | 43 tests: 40 pasados, 3 fallados | ⚠️ 3 fallados menores (clave adherence, enum VitalType, batch vacío) |
| OpenAPI/Swagger | `/docs` y `/api/v1/openapi.json` | ✅ Disponible |
| Infraestructura | Plantillas Bicep en `infra/azure/` | ✅ Completo |

**Brechas críticas Backend:**
- 3 tests fallando en `test_medications.py` y `test_vitals_comprehensive.py`
- Falta validación de enum `VitalType` en `VitalReadingCreate`
- Falta validación de lista vacía en endpoint `/batch`

### 8.2 Frontend-App (`Github/Frontend-App`)

| Área | Qué se validó | Resultado |
|------|--------------|-----------|
| Estructura del repositorio | 86 archivos Dart en `lib/`, 21 archivos de prueba | ✅ Completa |
| Pantallas implementadas | Home, Salud, Check-in, Observaciones, Alertas, SOS, Chat, Medicación, Documentos, Adulto Mayor | ✅ Todas las clave implementadas |
| Navegación (go_router) | ~40 rutas configuradas | ⚠️ Ruta `/health` no registrada (bug crítico) |
| Gestión de estado (Riverpod) | Dual Repository (Http + Mock) | ✅ Implementado |
| Pruebas (flutter test) | 73 tests, 100% pasando | ✅ Completo |
| Análisis estático (flutter analyze) | 0 errores, 0 warnings | ✅ Limpio |

**Brechas críticas Frontend:**
- **Ruta `/health` no registrada** en `app_router.dart` → `FamilyHomeScreen` llama `context.push('/health')` y falla en runtime
- **`useMocks` default = true** en `app_config.dart` → la app usa mocks por defecto en lugar de API real
- Pantalla de configuración de umbrales faltante (modelo existe, UI no)
- Perfil de paciente dedicado faltante (modelo existe, UI no)

---

## 9. Matriz de Alineación: Código Real vs. Roadmap Alloxentric

| Contenido Sprint 3 (Alloxentric) | ¿Backend? | ¿Frontend? | ¿Listo para Demo? | Acción |
|----------------------------------|-----------|------------|-------------------|--------|
| API ingesta de vitals (AGE-301) | ✅ Sí | N/A | ✅ Sí | Mantener |
| API series y umbrales (AGE-302) | ✅ Sí | N/A | ✅ Sí | Mantener |
| API semáforo del día (AGE-303) | ✅ Sí | N/A | ✅ Sí | Mantener |
| Pantalla Salud con tendencias (AGE-304) | N/A | ✅ Sí | ⚠️ Falta ruta `/health` | Corregir ruta |
| Pantalla Inicio con semáforo (AGE-305) | N/A | ✅ Sí | ✅ Sí | Mantener |
| Simulador de wearable (AGE-306) | N/A | ✅ Sí | ✅ Sí | Mantener |
| Web admin: semillas y datos demo (AGE-307) | ❌ No | N/A | ❌ Faltante | Evaluar si es Must |
| Web admin: umbrales por defecto (AGE-308) | ❌ No | N/A | ❌ Faltante | Evaluar si es Must |

---

## 10. Riesgos y Mitigaciones

| Riesgo | Impacto | Mitigación |
|--------|---------|------------|
| **Scope creep** (solicitudes Alloxentric fuera del goal) | Alto | Registrar en Product Backlog para sprints futuros; NUNCA improvisar requerimientos fuera del Sprint Goal en curso |
| **Sobrecarga del Scrum Master** (revisar todos los PRs) | Alto | Delegar revisión técnica a Agent 3 (QA) para PRs de bajo riesgo; enfocarse en revisión final y trazabilidad |
| **Dependencia API↔UI** | Medio | Usar mocks del backend mientras se desarrolla el frontend; integrar una vez el endpoint esté verde |
| **No llegar al demo funcional** | Crítico | Priorizar Must sobre Should/Could; entregar algo simple que funcione en lugar de algo complejo incompleto |
| **Tests fallando en backend** | Medio | Corregir los 3 tests fallando en Semana 1 antes de marcar cualquier historia como Done |
| **Ruta `/health` no funcional** | Alto | Corregir en Día 1 de Semana 1; es bloqueante para el demo del semáforo |

---

## 11. Criterios de Éxito al Final de las 4 Semanas

| Métrica | Objetivo |
|---------|----------|
| Historias completadas con DoD | 8–10 historias |
| Puntos entregados | 35–45 Fibonacci |
| Tests en verde | 100% de las historias entregadas |
| Demo funcional | Vitals + semáforo + check-in + observaciones + alertas básicas |
| Trazabilidad Jira-Git | 100% de historias con PR vinculado y comentario en Jira (`@ce.gacitua`) |
| Evidencia académica | Sprint reports, diagnóstico de código, documentación actualizada para RA1–RA3 |

---

## 12. Alineación con Resultados de Aprendizaje (RA) DUOC UC

| RA | Descripción | Evidencia en este plan |
|----|-------------|----------------------|
| **RA1** | Diseña una propuesta de proyecto con competencias de egreso | Pirámide de valor, matriz MoSCoW, planificación de 4 semanas, estimación Fibonacci, gestión de riesgos |
| **RA2** | Desarrolla el Proyecto APT según estándares de calidad | DoR/DoD, Vertical Slicing, pruebas 100% verde, arquitectura limpia, IaC Bicep, trazabilidad Git/Jira |
| **RA3** | Presenta el Proyecto APT con evidencias de competencias | Este documento, diagnóstico de código (Fase 0), sprint reports, registros de uso IA, documentación técnica |

---

## 13. Comandos de Referencia Rápida

```bash
# Diagnóstico general del workspace AgeCare
./.agents/agecare-scrum doctor

# Ejecutar pruebas en Backend FastAPI
cd /home/extropyst/Documentos/Capstone/AgeCare/Github/Backend-API && pytest -v

# Ejecutar análisis y pruebas en Frontend Flutter
cd /home/extropyst/Documentos/Capstone/AgeCare/Github/Frontend-App && flutter analyze && flutter test

# Ver estado de branches en todos los repositorios
for r in Backend-API Frontend-App Docs; do git -C "/home/extropyst/Documentos/Capstone/AgeCare/Github/$r" status -s -b; done
```

---

## 14. Próximo Paso Inmediato

**Hoy mismo (Día 1 de Semana 1):**

1. Ejecutar la Fase 0 de diagnóstico de código (ya completada — ver sección 8)
2. Crear los 10 issues en Jira (ya creados: DAC05-222 a DAC05-231)
3. Crear las 19 subtareas en Jira (ya creadas: DAC05-232 a DAC05-250)
4. Iniciar el desarrollo de la primera historia (DAC05-222: API ingesta de vitals)
5. Crear rama: `git checkout -b feature/DAC05-222-api-ingesta-vitals`

---

*Documento generado por `agecare-scrum-master` (v1.0.0) — Scrum Master, Agile Coach y Asesor Metodológico Principal del Proyecto AgeCare*

**Última actualización:** 29 de octubre de 2026

**Almacenamiento local:** `/home/extropyst/Documentos/Capstone/AgeCare/Documentos del Equipo/Plan de Realineamiento y Priorización — 4 Semanas Restantes.md`

**Sincronización Confluence:** Documentos creados en espacios SSOT y DAC05 (ver sección de documentos creados en la sesión anterior)

**Sincronización GitHub:** Pendiente — se puede subir a `Github/Docs/Fase 2/Evidencias Grupales/` posteriormente