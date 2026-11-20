# Estructura Sugerida — Presentación PPT Entrega Final Fase 2

**Archivo base:** `AgeCare_Digital_Command_Center.pptx` (copiado de Fase 3, requiere refinamiento)
**Fecha de entrega:** 20 de noviembre de 2026
**Presentador:** César Gacitúa (@ce.gacitua)

---

## Diapositivas Sugeridas

### 1. Portada
- Título: AgeCare — Sistema de Cuidado y Asistencia para Adultos Mayores
- Subtítulo: Entrega Final — Fase 2 | Proyecto de Título APT122
- Presentador: César Gacitúa
- Fecha: 20 de noviembre de 2026
- Contraparte: Alloxentric / Wellq Co
- Institución: DUOC UC — Sede Antonio Varas

### 2. Visión del Proyecto y Propuesta de Valor
- Plataforma integral de cuidado y asistencia para personas mayores y cuidadores a distancia
- Alineada con Ley 21.805 (Chile Cuida)
- Modelo Freemium: el adulto mayor nunca paga
- Centro de mando tranquilizador para el familiar responsable

### 3. Arquitectura del Sistema
- Frontend: Flutter / Dart (Clean Architecture, Riverpod, go_router, Material 3)
- Backend: FastAPI (Python, asyncpg, Pydantic v2, PostgreSQL)
- Infraestructura: Microsoft Azure (Container Apps, PostgreSQL Flexible Server, Bicep IaC)
- Notificaciones: Firebase Cloud Messaging (FCM)

### 4. Roles del Sistema
- Familiar (responsable a distancia)
- Cuidadora
- Médico
- Adulto Mayor (interfaz accesible, voz primero)

### 5. Funcionalidades Clave (MVP v1)
- Monitoreo de signos vitales (wearables)
- Gestión estricta de medicamentos
- Comunicación asistida por IA
- Círculo de cuidado (invitación por código de 6 dígitos, expiración 48h)
- Alarmas locales de medicación

### 6. Avance Técnico — Backend
- API RESTful con FastAPI
- Base de datos PostgreSQL con migraciones Alembic
- Autenticación y autorización (RBAC)
- Endpoints implementados y probados con pytest
- Despliegue en Azure Container Apps

### 7. Avance Técnico — Frontend
- App móvil Flutter con Clean Architecture por feature
- Gestión de estado con Riverpod
- Navegación con go_router
- Material 3 y diseño accesible
- Pruebas unitarias y de widgets con flutter test

### 8. Infraestructura y DevOps
- IaC con Bicep para Azure
- CI/CD con GitHub Actions
- PostgreSQL Flexible Server (Standard_B1ms)
- Key Vault para secretos
- Container Apps para el backend

### 9. Evidencias de Sistema (Aplicación / Base de Datos)
- [Insertar capturas de pantalla de la app funcionando]
- [Insertar capturas de la base de datos PostgreSQL]
- [Insertar capturas del despliegue en Azure]

### 10. Metodología Ágil — Scrum
- Sprints planificados y ejecutados
- Historias de usuario con formato INVEST y BDD Gherkin
- Trazabilidad Jira ↔ GitHub
- Definición de Hecho (DoD) y Definición de Listo (DoR) cumplidas

### 11. Registro de Uso de IA (Normativa Capstone 2026-1)
- Herramientas utilizadas
- Prompts registrados en Git
- Revisión humana de todo código generado por IA
- Capacidad de defensa técnica individual

### 12. Conclusión y Próximos Pasos
- Estado actual del MVP v1
- Plan para Fase 3 (Presentación Final: 04 de diciembre)
- Mejoras identificadas para versiones futuras

---

## Notas para el Refinamiento del PPT

1. **Actualizar datos técnicos** con los endpoints reales implementados en el backend FastAPI
2. **Incluir capturas de pantalla** de la aplicación Flutter funcionando (pendiente de captura por el usuario)
3. **Incluir capturas de la base de datos** PostgreSQL (pendiente de captura por el usuario)
4. **Verificar que todos los diagramas estén actualizados** (arquitectura, ERD, flujo de navegación)
5. **Mantener consistencia visual** con Material 3 y la identidad de AgeCare
6. **Incluir menciones al equipo** y roles individuales
