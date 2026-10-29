# 📚 AgeCare — Documentación Técnica y Evidencias Académicas

Repositorio oficial de documentación del proyecto **AgeCare** — Plataforma digital de cuidado y acompañamiento de adultos mayores.

Desarrollado en el marco del **Proyecto Capstone** de la carrera de Ingeniero Informático en **DUOC UC**, Escuela de Informática y Telecomunicaciones, en colaboración con **Alloxentric / Wellq Co**.

---

## 🎯 Propósito de este Repositorio

Este repositorio contiene toda la documentación formal, evidencias técnicas y entregables académicos del proyecto AgeCare, organizados por fases del ciclo de titulación DUOC UC (RA1, RA2, RA3).


---

## 📂 Estructura de la Documentación

```
Docs/
├── Fase 1/          # RA1 — Definición de requerimientos y arquitectura
├── Fase 2/          # RA2 — Avance de implementación e informe técnico
├── Fase 3/          # RA3 — Preparación para comisión de titulación
└── README.md        # Este archivo
```

### Fase 1 — RA1: Definición
- Requerimientos funcionales y no funcionales
- Arquitectura de software
- Modelo de datos y diseño de API
- Historias de usuario y criterios de aceptación

### Fase 2 — RA2: Avance
- Informe de avance de implementación
- Evidencias de desarrollo (código, pruebas, despliegue)
- Métricas de flujo (velocity, burndown, cycle time)
- Retrospectivas de sprint

### Fase 3 — RA3: Comisión
- Informe final de titulación
- Preparación para exposición ante comisión
- Evidencias de cumplimiento de rúbricas DUOC UC
- Lecciones aprendidas y mejoras futuras

---

## 🔗 Repositorios de la Organización

| Repositorio | Descripción | Stack Principal |
| :--- | :--- | :--- |
| [`Backend-API`](https://github.com/AgeCare-DUOC/Backend-API) | Backend oficial: API REST y WebSockets | FastAPI, Python 3.12, PostgreSQL, Azure |
| [`Frontend-App`](https://github.com/AgeCare-DUOC/Frontend-App) | Frontend móvil y web multiplataforma | Flutter, Dart, Riverpod, Material 3 |


---

## 🛠️ Stack Tecnológico Documentado

### Backend (AgeCare Core API)
- **Framework:** FastAPI (Python 3.12+)
- **Validación:** Pydantic v2
- **Base de Datos:** PostgreSQL (Azure Database for PostgreSQL Flexible Server) vía SQLAlchemy 2.0 Async (`asyncpg`)
- **Migraciones:** Alembic
- **Seguridad:** JWT Bearer y `bcrypt`
- **Integraciones:** Alloxentric Speech-to-Text & NLP, Azure Blob Storage, WebSockets

### Frontend (CapstoneAgecare)
- **Framework:** Flutter / Dart (Clean Architecture por feature)
- **Gestión de estado:** Riverpod
- **Navegación:** `go_router`
- **Diseño:** Material 3, interfaz accesible y voice-first

### DevOps y Calidad
- **CI/CD:** GitHub Actions
- **IaC:** Bicep (Azure)
- **Testing:** `pytest` (backend), `flutter test` (frontend)
- **Análisis estático:** `flutter analyze`, `pylint` / `ruff`

---

## 📋 Gobernanza Ágil

### Definición de Listo (DoR)
- Historias de usuario bajo formato INVEST
- Escenarios de aceptación BDD/Gherkin (2-4 escenarios)
- Estimación en escala Fibonacci (1, 2, 3, 5, 8, 13)
- Vertical slicing: corte vertical end-to-end (UI + API + DB)

### Definición de Hecho (DoD)
- Tests en verde (`pytest` / `flutter test`)
- Análisis estático limpio (`flutter analyze`)
- Peer Review aprobado en Pull Request
- Trazabilidad Jira ↔ Git con clave `DAC05-XX`

---

## 📄 Licencia

Este proyecto se desarrolla como parte del título de Ingeniero Informático en DUOC UC. Consulta el archivo `LICENSE` para los términos de uso específicos.

---

<div align="center">

**AgeCare — Tranquilidad a Distancia** 💙

*Proyecto Capstone DUOC UC · Alloxentric / Wellq Co · Octubre 2026*

</div>