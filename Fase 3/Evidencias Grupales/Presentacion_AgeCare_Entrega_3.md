---
title: "AgeCare: Sistema Integral de Teleasistencia y Cuidado para Personas Mayores"
subtitle: "Presentación Final / Avance — Asignatura Capstone (DUOC UC / Alloxentric)"
author: "César Gacitúa (Scrum Master & Lead Engineer)"
date: "Octubre / Noviembre 2026"
lang: "es"
---

# Diapositiva 1: Portada

## PROYECTO "AGECARE" | PRESENTACIÓN FINAL CAPSTONE
- **Sistema Integral de Teleasistencia y Cuidado para Personas Mayores**
- **Contraparte Empresarial:** Alloxentric / Wellq Co
- **Institución:** DUOC UC — Sede Antonio Varas (Ingeniería en Informática)
- **Autor / Integrante:** César Gacitúa (`@ce.gacitua`)
- **Fecha:** Octubre / Noviembre 2026

---

# Diapositiva 2: Tecnologías Utilizadas

## Tecnologías Utilizadas (Propósito de Negocio)
- **Flutter (Dart):** Interfaz móvil y web multiplataforma, accesible y de alto contraste para personas mayores y cuidadores.
- **FastAPI (Python):** API REST asíncrona de alto rendimiento para el procesamiento de datos clínicos y alertas.
- **PostgreSQL:** Base de datos relacional segura para el almacenamiento del expediente clínico y lecturas vitales.
- **Microsoft Azure:** Nube empresarial (Container Apps y PostgreSQL Flexible Server) para alta disponibilidad.
- **Alembic:** Gestor de migraciones que actualiza la estructura de la base de datos sin comprometer ni borrar la información histórica de los pacientes.
- **Alloxentric Voice Engine:** Motor de transcripción de notas de voz y notas de relevo de turno.

---

# Diapositiva 3: Demostración en Vivo

## DEMOSTRACIÓN DEL RESULTADO DEL PROYECTO
**Exposición del Sistema en Vivo (~5-6 minutos):**
1. **Inicio y Semáforo de Bienestar (`DAC05-223`):** Dashboard del familiar con estado integral (`ok`, `warning`, `critical`).
2. **Pantalla de Salud y Tendencias (`DAC05-222`):** Navegación a `/health`, tarjetas de signos vitales (FC, SpO2, Temperatura) y selector temporal 7/30/90 días.
3. **Simulador de Wearable (`DAC05-226`):** Inyección en lote de lecturas (`POST /vitals/batch`) y eventos críticos (SpO2 bajo / caída).
4. **Umbrales de Alerta (`DAC05-279`):** Configuración personalizada de rangos con validación matemática en tiempo real (`min < max`).
5. **Plan de Medicamentos y Adherencia (`DAC05-285` & `DAC05-286`):** Configuración de dosis por el médico/cuidadora y confirmación de tomas por la cuidadora con actualización instantánea de adherencia.

---

# Diapositiva 4: Resultados Obtenidos

## Resultados Obtenidos
- **Arquitectura E2E Integrada:** Conexión asíncrona fluida entre Flutter, FastAPI y PostgreSQL.
- **Núcleo de Salud Operativo:** Ingesta de signos vitales, semáforo automatizado y gráficas de tendencias históricas.
- **Módulo de Medicamentos y Adherencia:** Ciclo completo desde la prescripción hasta la confirmación de tomas.
- **Calidad Validada:** 100% de pruebas unitarias y de integración en verde (`63/63 pytest`, `109/109 flutter test`).

---

# Diapositiva 5: Obstáculos y Resiliencia Técnica

## Obstáculos Presentados durante el Desarrollo
- **Desacoplamiento de SDKs de Wearables:** Resuelto mediante el patrón Adapter con la interfaz abstracta `WearableSource`, permitiendo alternar entre simulación y hardware real sin romper la Clean Architecture.
- **Concurrencia en Ingesta Masiva:** Mitigado mediante constraints de idempotencia en base de datos (`uq_vital_reading_idempotent`) para prevenir duplicidad ante reintentos de red.
- **Estabilización de Pruebas (NixOS):** Resuelto mediante inyección de librerías nativas (`libstdc++.so.6`) para garantizar la ejecución exitosa de `pytest`.

---

# Diapositiva 6: Preguntas

## PREGUNTAS DE LA COMISIÓN
- Espacio abierto para resolver dudas técnicas, metodológicas o de negocio.
- **¡Muchas gracias por su atención!**

---

# Diapositiva 7: Integrantes

## INTEGRANTES DEL PROYECTO
- **César Gacitúa:** Scrum Master, Agent Orchestrator y Product Owner (HITL).
- *Nota metodológica:* Desarrollo soportado mediante ingeniería agéntica especializada (Backend, Frontend, QA/DevOps) bajo estricta revisión humana y cumplimiento de DoD.

---

# Diapositiva 8: Descripción del Proyecto

## DESCRIPCIÓN DEL PROYECTO (Problema y Solución)
- **Problema / Dolor:** Los familiares responsables que cuidan a adultos mayores a distancia sufren de ansiedad constante por no saber si sus seres queridos están bien, si tomaron sus medicamentos o si sufrieron una emergencia médica.
- **Propuesta de Solución:** AgeCare es una plataforma de teleasistencia integrada que ofrece un centro de mando tranquilizador ("Hoy"), monitoreo automatizado de signos vitales, semáforo de bienestar y gestión estricta de adherencia farmacológica, alineada con la Ley 21.805 (*Chile Cuida*).

---

# Diapositiva 9: Objetivos

## OBJETIVOS DEL PROYECTO
- **Objetivo General:** Desarrollar una plataforma tecnológica de teleasistencia y monitoreo remoto para adultos mayores que brinde paz mental a los familiares a través de trazabilidad de salud y adherencia farmacológica.
- **Objetivos Específicos:**
  1. Implementar la ingesta y visualización de signos vitales (wearable y manual).
  2. Automatizar el cálculo de un semáforo de bienestar en tiempo real.
  3. Gestionar planes de medicamentos y registro de adherencia por roles.
  4. Garantizar estándares de calidad industrial (Clean Architecture, CI/CD, IaC Azure).

---

# Diapositiva 10: Alcance y Limitaciones

## ALCANCE Y LIMITACIONES DEL PROYECTO
- **Alcance Funcional (MVP):**
  - Autenticación segura y gestión de pacientes.
  - Módulo de salud: signos vitales, semáforo, umbrales y tendencias.
  - Módulo de medicación: plan de medicamentos, agenda de tomas y adherencia.
  - Operación de cuidadoras (check-in y observaciones).
- **Limitaciones:**
  - El sistema no emite diagnósticos médicos automáticos (es un soporte de teleasistencia).
  - El adulto mayor utiliza una interfaz accesible sin fricción de credenciales (modelo Freemium: el adulto mayor nunca paga).
  - No incluye pasarela de pago para la marketplace en esta fase académica.

---

# Diapositiva 11: Metodología

## METODOLOGÍA DE TRABAJO
- **Marco:** Scrum Empírico (Iteraciones de 2 semanas / Sprints).
- **Gobernanza de Requisitos:** Historias de usuario bajo estándar INVEST y escenarios BDD Gherkin.
- **Vertical Slicing ("Corte de Torta"):** Cada historia atraviesa todas las capas (UI Flutter + API FastAPI + DB PostgreSQL), prohibiendo épicas técnicas horizontales.
- **Definición de Hecho (DoD):** Pruebas 100% en verde, análisis estático limpio, infraestructura Bicep validada y trazabilidad Git-Jira.

---

# Diapositiva 12: Cronograma

## CRONOGRAMA DE EJECUCIÓN (4 Semanas)
| Fase / Hito | Período | Estado |
|---|---|---|
| **Definición y Fase 0 (Diagnóstico)** | Semana 1 | ✅ Finalizado |
| **Sprint 3: Núcleo de Salud + Medicamentos** | Semana 2 | ✅ Finalizado (100% Done) |
| **Sprint 4: Operación de la Cuidadora (Check-in/Tareas)** | Semana 3 | 🔄 En ejecución |
| **Sprint 5 & 6: Alertas, SOS, Regresión y Demo Final** | Semana 4 | 📅 Planificado |

---

# Diapositiva 13: Arquitectura

## ARQUITECTURA DEL SOFTWARE
- **Frontend (Flutter):** Clean Architecture por feature (`presentation` → `domain` ← `data`).
- **Backend (FastAPI):** Arquitectura en capas asíncrona (`routers` → `crud` → `db`).
- **Infraestructura (Azure):** Azure Container Apps + PostgreSQL Flexible Server mediante IaC (Bicep).
- *Nota clave:* Las flechas de dependencia fluyen estrictamente desde la UI hacia el dominio y los datos, manteniendo el núcleo de negocio desacoplado de frameworks externos.

---

# Diapositiva 14: Modelo de Datos

## MODELO DE DATOS (Esquema Estrella)
- **Nomenclatura Consistente:** Entidades relacionales en inglés normalizado (`patients`, `vital_readings`, `vital_thresholds`, `medication_plans`, `scheduled_doses`, `medication_intakes`).
- **Diseño Tipo Estrella:**
  - **Tabla de Hechos (Fact):** `vital_readings` (registros temporales de signos vitales) y `medication_intakes` (administración de dosis).
  - **Tablas de Dimensión:** `patients` (adulto mayor), `users` (familiares, cuidadores, médicos), `vital_thresholds` (umbrales de alerta).
- **Integridad:** Claves foráneas con borrado en cascada (`ON DELETE CASCADE`) e índices compuestos optimizados para consultas históricas en milisegundos.
