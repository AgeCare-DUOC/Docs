# Presentación: AgeCare - Presentación 1

## Diapositiva 1: Diapositiva 1

- PROYECTO AGECARE
- PRESENTACIÓN FINAL CAPSTONE

---

## Diapositiva 2: Diapositiva 2

- PROYECTO AGECARE
- INTEGRANTES DEL PROYECTO

---

## Diapositiva 3: Diapositiva 3

- PROYECTO AGECARE
- DESCRIPCIÓN DEL PROYECTO
- Problema o dolor
- Poco orden y comunicación en el monitoreo de salud, las alertas, la coordinación del cuidado y la comunicación entre familiares, cuidadores y médicos de un adulto mayor en plena era digital. Poca oferta de espacios centralizados para familiares de adultos mayores a distancia.
- Propuesta de solución
- Proporcionar a las familias información confiable y en tiempo real sobre el bienestar de su ser querido, y al adulto mayor un medio accesible para mantenerse conectado, acompañado y activo. Ficha clínica digital.

---

## Diapositiva 4: Diapositiva 4

- PROYECTO AGECARE
- Objetivo General
- Objetivos Específicos
- Desarrollar una plataforma digital integral de cuidado de adultos mayores que centralice el monitoreo de salud, las alertas, la coordinación del cuidado y la comunicación entre familiares, cuidadores, médicos y el propio adulto mayor, con el fin de proporcionar a las familias que cuidan a distancia información confiable y en tiempo real sobre el bienestar de su ser querido, y al adulto mayor un medio accesible para mantenerse conectado, acompañado y activo.
- Consolidar en un expediente único y compartido la información de salud del adulto mayor —signos vitales del wearable, adherencia a medicamentos, observaciones de la cuidadora, incidentes y documentos médicos—, presentada mediante un semáforo de bienestar diario por paciente y con soporte multi-paciente.
- Implementar un sistema de alertas en tiempo real, con notificaciones push y umbrales configurables, que detecte y comunique los eventos críticos del cuidado: caída detectada, signo vital fuera de rango y medicamento no administrado, incluyendo un flujo de acción inmediata ante caídas y un botón SOS.
- Gestionar el ciclo completo de la medicación: definición del plan por la cuidadora o el médico, digitalización de recetas mediante OCR, alarmas de tomas, confirmación de dosis y visualización de la adherencia por parte del familiar.

---

## Diapositiva 5: Diapositiva 5

- PROYECTO AGECARE
- Alcance y limitaciones del proyecto
- Alcance: Desarrollo de frontend de aplicación móvil.
- Este plan lleva la versión 1 completa de AgeCare desde cero hasta el envío a App Store y Google Play en 10 semanas (2.5 meses), con un piloto con usuarios reales a partir de la semana 8. El alcance cubre todo el documento de funcionalidades v1: monitoreo de salud, alertas, medicamentos, comunicación (chat + asistente IA), vista del adulto mayor, vista de la cuidadora con freemium, marketplace vitrina y web de administración.
- Limitaciones: Desarrollo de backend por parte de otro grupo, dependencias

---

## Diapositiva 6: Diapositiva 6

- PROYECTO AGECARE
- Metodología de trabajo para el desarrollo del proyecto
- Scrum con sprints semanales, alineados a los tickets ya definidos por la empresa (Alloxentric/Wellq Co) en su Plan de Desarrollo v1 — no redactamos historias desde cero, tomamos los tickets identificados como AGE-XXX que corresponden al rol APP/APP-R (frontend móvil), ya que backend y panel web los desarrolla otro equipo.
- Trabajo organizado por épica (EP-02 Autenticación, EP-04 Vitals/wearable, EP-05 Medicamentos, EP-06 Alertas/SOS, EP-07 Bitácora, EP-08 Chat, EP-09 Asistente IA, EP-10 Vista adulto mayor, EP-11 Cuidadora/freemium), cada una con sus tickets ya especificados (criterios de aceptación incluidos).
- Ceremonias: planning semanal, daily stand-up corto (async si no calza el horario), review/demo al cierre del sprint, retrospectiva.
- Seguimiento en Jira (tablero SCRUM) y versionado en Git (rama por ticket, PR revisado antes de integrar).
- Desarrollo contra mocks primero (USE_MOCKS=true, ya incluido en el código base) mientras el equipo de backend entrega la API real descrita en la
- Especificación de Endpoints v1; migración a USE_MOCKS=false cuando el endpoint correspondiente esté disponible.
- Entregas continuas: build de demostración desplegada (Flutter Web) para que la empresa monitoree el avance entre reuniones, según lo acordado en la primera reunión con Alloxentric.
- Entregas continuas: build de demostración desplegada (Flutter Web) para que la empresa monitoree el avance entre reuniones, según lo acordado en la primera reunión con Alloxentric.

---

## Diapositiva 7: Diapositiva 7

- PROYECTO AGECARE
- Cronograma o Release Plan para el desarrollo del proyecto
- * Utilizar cronograma de inicio, indicando el cumplimiento al término del proyecto

---

## Diapositiva 8: Diapositiva 8

- PROYECTO AGECARE
- Arquitectura del software
- Arquitectura ya definida en el código base (agecare_app), por capas dentro de cada feature:
- Presentation — pantallas y widgets (Material 3, tokens de diseño en core/theme/app_theme.dart).
- Application — providers de Riverpod (FutureProvider para lecturas, Notifier para estado global como sesión y paciente seleccionado).
- Domain — modelos de datos de cada feature.
- Data — patrón Repository con dos implementaciones intercambiables: ...Http (backend real) y ...Mock (datos en memoria), seleccionadas por AppConfig.useMocks.
- Navegación: go_router, con control de sesión y rutas de detalle; MainShell decide la navegación inferior según el rol (familiar, cuidadora, adulto mayor).
- Red: dio encapsulado en ApiClient — agrega prefijo /api/v1, bearer token, y renueva el access token automáticamente ante un 401.
- Integraciones externas: Spike SDK (wearables), Firebase/FCM + notificaciones locales (alertas y recordatorios de medicación), flutter_secure_storage (tokens).

---

## Diapositiva 9: Diapositiva 9

- PROYECTO AGECARE
- Modelo de datos

---

## Diapositiva 10: Diapositiva 10

- PROYECTO AGECARE
- Tecnologías utilizadas
- Frontend: App móvil (nuestro alcance)
- Flutter (iOS y Android)
- Riverpod - gestión de estado
- go_router - navegación por rol
- dio - cliente HTTP (token JWT, auto-renovación)
- Spike SDK - integración con wearables
- Firebase / FCM - notificaciones push
- flutter_secure_storage -  almacenamiento seguro de credenciales
- Backend: contrato consumido (otro equipo)
- FastAPI (Python 3.12) + PostgreSQL (Azure)
- Autenticación JWT
- Azure AI Document Intelligence - OCR de recetas
- LLM (Azure OpenAI / Claude) - asistente IA
- Entrega continua
- Git + GitHub Actions
- Build de demostración en Vercel

---

## Diapositiva 11: Diapositiva 11


> **Notas del Orador:**
> https://www.figma.com/make/Rg7cx49DWyUHHhQ1Ua1FBI/AGECARE---Primeros-mock-ups?t=eccnN7TypQvwRhCn-0

---

## Diapositiva 12: Diapositiva 12


> **Notas del Orador:**
> https://www.figma.com/make/Rg7cx49DWyUHHhQ1Ua1FBI/AGECARE---Primeros-mock-ups?t=eccnN7TypQvwRhCn-0

---

## Diapositiva 13: Diapositiva 13

- DEMOSTRACIÓN DEL RESULTADO DEL PROYECTO
- *Exposición del sistema

---

## Diapositiva 14: Diapositiva 14

- Resultados obtenidos

---

## Diapositiva 15: Diapositiva 15

- Obstáculos presentados durante el desarrollo

---

## Diapositiva 16: Diapositiva 16

- PREGUNTAS DE LA COMISIÓN
