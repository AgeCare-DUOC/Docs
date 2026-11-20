# Presentación: AgeCare_Presentacion_final_1

## Diapositiva 1: Diapositiva 1

- PRESENTACIÓN FINAL CAPSTONE
- AgeCare
- Cuidado conectado para adultos mayores y sus familias
- Ingeniería en Informática · Escuela de Informática y Telecomunicaciones

---

## Diapositiva 2: Equipo del proyecto

- CI
- Claudia Iosue
- Scrum Master
- Facilita las ceremonias y el avance de los sprints
- FB
- Franco Barra
- QA
- Asegura la calidad de cada entrega
- CG
- César Gacitua
- Backend developer / DevOps
- Trabaja en backend
- FV
- Felipe Varas
- Frontend developer
- Construye la app móvil en Flutter
- Empresa: Alloxentric
- ‹#›

---

## Diapositiva 3: Descripción del proyecto

- El problema
- Poco orden y comunicación en el monitoreo de salud, las alertas, la coordinación del cuidado y la comunicación entre familiares, cuidadores y médicos de un adulto mayor en plena era digital. Poca oferta de espacios centralizados para familiares de adultos mayores a distancia.
- Nuestra propuesta
- Proporcionar a las familias información confiable y en tiempo real sobre el bienestar de su ser querido, y al adulto mayor un medio accesible para mantenerse conectado, acompañado y activo. Ficha clínica digital.
- UNA APP, CUATRO ROLES
- Familiar
- Cuidadora
- Adulto mayor
- Médico
- ‹#›

---

## Diapositiva 4: Objetivos

- OBJETIVO GENERAL
- Desarrollar una plataforma digital integral de cuidado de adultos mayores que centralice el monitoreo de salud, las alertas, la coordinación del cuidado y la comunicación entre familiares, cuidadores, médicos y el propio adulto mayor, con el fin de proporcionar a las familias que cuidan a distancia información confiable y en tiempo real sobre el bienestar de su ser querido, y al adulto mayor un medio accesible para mantenerse conectado, acompañado y activo.
- Expediente único
- Consolidar la información de salud del adulto mayor —signos vitales del wearable, adherencia a medicamentos, observaciones de la cuidadora, incidentes y documentos médicos— en un expediente compartido, con semáforo de bienestar diario y soporte multi-paciente.
- Alertas en tiempo real
- Notificaciones push con umbrales configurables ante eventos críticos: caída detectada, signo vital fuera de rango y medicamento no administrado. Incluye flujo de acción inmediata ante caídas y botón SOS.
- Ciclo de medicación
- Plan definido por la cuidadora o el médico, digitalización de recetas mediante OCR, alarmas de tomas, confirmación de dosis y visualización de la adherencia por parte del familiar.
- ‹#›

---

## Diapositiva 5: Alcance y limitaciones

- 5
- sprints de dos semanas: 10 semanas (2,5 meses) para la versión 1
- 4
- sprint en que comienza el piloto con usuarios reales
- 2
- tiendas de destino: App Store y Google Play
- Nuestro alcance: frontend de la aplicación móvil
- Monitoreo de salud
- Alertas
- Medicamentos
- Chat + asistente IA
- Vista adulto mayor
- Vista cuidadora (freemium)
- Marketplace vitrina
- Limitaciones
- Backend y web de administración a cargo de otro equipo.
- Dependencia de la entrega de endpoints: avanzamos con mocks mientras la API real está disponible.
- ‹#›

---

## Diapositiva 6: Metodología: Scrum

- Trabajamos sobre los tickets AGE-XXX ya definidos por Alloxentric / Wellq Co en su Plan de Desarrollo v1 (rol APP/APP-R, frontend móvil), cada uno con criterios de aceptación. No redactamos historias desde cero.
- 01
- Planning
- Al inicio de cada sprint
- 02
- Daily stand-up
- Corto, async si no calza el horario
- 03
- Review / demo
- Al cierre del sprint
- 04
- Retrospectiva
- Mejora continua del equipo
- Ciclo que se repite en cada uno de los 5 sprints
- ‹#›

---

## Diapositiva 7: Flujo de desarrollo y entregas

- Ticket en Jira
- Tablero SCRUM
- Rama por ticket
- Versionado en Git
- Pull request
- Revisado antes de integrar
- Integración
- GitHub Actions
- Build de demo
- Flutter Web en Vercel
- Entregas continuas
- Una build de demostración desplegada permite que la empresa monitoree el avance entre reuniones, según lo acordado en la primera reunión con Alloxentric.
- ‹#›

---

## Diapositiva 8: Cronograma: release plan

- 1
- Sprint 1
- Semanas 1–2
- Setup
- Autenticación y navegación
- 2
- Sprint 2
- Semanas 3–4
- Vitals / wearable
- Medicamentos
- 3
- Sprint 3
- Semanas 5–6
- Alertas / SOS
- Bitácora / OCR
- 4
- Sprint 4
- Semanas 7–8
- Chat / asistente IA
- Vista adulto mayor
- 5
- Sprint 5
- Semanas 9–10
- Marketplace
- QA final
- Piloto con usuarios · semana 8
- Entrega final · semana 10
- ‹#›

---

## Diapositiva 9: Arquitectura del software

- Clientes
- App Flutter
- Android · iOS · Riverpod · Dio
- Versión web
- Flutter web · Vercel
- Azure · Brazil South
- REST /api/v1 + JWT · WebSocket chat
- Core API
- FastAPI · Python 3.12 · App Service
- PostgreSQL 16
- SQLAlchemy 2 · asyncpg · Alembic
- Blob Storage
- Fotos, audios y documentos · URL SAS
- Servicios externos
- Firebase FCM
- Notificaciones push
- Claude API
- Asistente IA y recetas
- Azure AI Speech
- Dictado y lectura en voz
- Spike API
- Wearables
- CI/CD:  GitHub Actions · Docker / docker-compose · deploy.ps1 → Azure App Service
- ‹#›

---

## Diapositiva 10: Modelo de datos

- care_tasks
- Tareas de cuidado
- +1
- vital_readings
- Signos vitales
- +1
- medications
- Plan de medicamentos
- +2
- scheduled_doses
- Dosis programadas
- users
- Cualquier persona
- +6
- patient_members
- Rol en cada paciente
- patients
- Expediente
- +3
- alerts
- Alertas
- sos_events
- Eventos SOS
- caregiver_profiles
- Perfil de cuidadora
- +10
- observations
- Bitácora diaria
- +3
- chat_messages
- Chat y asistente IA
- +7
- documents
- Documentos y archivos
- +1
- +N tablas de detalle que expanden la entidad
- Relación 1 a N (la flecha apunta al lado N)
- 13 entidades + 34 tablas de detalle = 47 tablas
- ‹#›

---

## Diapositiva 11: Tecnologías: app, backend y base de datos

- App
- Nuestro alcance
- Flutter 3 + Dart
- una sola base para Android, iOS y web
- Riverpod
- gestión de estado
- go_router
- navegación
- Dio
- cliente HTTP
- Backend
- Contrato consumido
- Python 3.12 + FastAPI
- framework de la API
- Pydantic v2
- validación de entradas y salidas
- JWT
- autenticación con access y refresh token
- argon2
- hash de contraseñas
- WebSocket
- chat en tiempo real
- OpenAPI / Swagger
- documentación en /docs
- Base de datos
- Persistencia
- PostgreSQL 16
- base de datos relacional
- SQLAlchemy 2
- ORM asíncrono
- asyncpg
- driver de PostgreSQL
- Alembic
- migraciones
- ‹#›

---

## Diapositiva 12: Tecnologías: infraestructura, servicios y DevOps

- Infraestructura
- Azure · Brazil South
- Azure App Service Linux
- API · plan B1
- Azure Database for PostgreSQL
- Flexible Server · plan B1ms
- Azure Blob Storage
- Standard LRS con URLs firmadas SAS
- Vercel
- versión web · plan Hobby
- Servicios externos
- Integraciones
- Firebase Cloud Messaging
- notificaciones push
- Claude API
- asistente IA y lectura de recetas
- Azure AI Speech
- dictado y lectura en voz alta
- Spike API
- integración con wearables
- DevOps y herramientas
- Repos, CI y despliegue
- GitHub
- los dos repositorios
- GitHub Actions
- integración continua (CI)
- PowerShell · deploy.ps1
- despliegue del backend
- Docker + docker-compose
- entorno local y entrega del frontend
- Mermaid
- diagramas de la página
- ‹#›

---

## Diapositiva 13: Prototipo de la aplicación

- Selección de rol
- Familiar, cuidadora, adulto mayor o médico
- Inicio del familiar
- Vitales, medicamentos del día y bitácora de la cuidadora
- Vista del adulto mayor
- Familia, fotos, entretenimiento y mensaje de voz
- ‹#›

> **Notas del Orador:**
> Prototipo en Figma: https://www.figma.com/make/Rg7cx49DWyUHHhQ1Ua1FBI/AGECARE---Primeros-mock-ups?t=eccnN7TypQvwRhCn-0

---

## Diapositiva 14: Diapositiva 14

- EN VIVO
- Demostración del sistema
- Recorrido por la app AgeCare

---

## Diapositiva 15: Resultados obtenidos

- ‹#›

---

## Diapositiva 16: Obstáculos durante el desarrollo

- ‹#›

---

## Diapositiva 17: Diapositiva 17

- ¿Preguntas?
- Preguntas de la comisión
- Claudia Iosue  ·  Franco Barra  ·  César Gacitua  ·  Felipe Varas
