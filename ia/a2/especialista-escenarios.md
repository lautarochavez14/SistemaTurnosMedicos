# Especialista en Escenarios de Casos de Uso (A2)

## Prompt Utilizado

**Prompt principal inicial:**
> Lee primero el archivo: anexos/introduccion.md y la plantilla PLANTILLA_ESCENARIO.md. Identifica 5 casos de uso relevantes del Sistema de Turnos Médicos y crea archivos individuales dentro de diagramas/03-escenarios-casos-de-uso/ usando exactamente el formato de la plantilla.

**Ajustes posteriores:**
Se refinaron los prompts para:
- Usar IDs en formato CU-01 a CU-05
- Mejorar el campo "Activar Evento"
- Corregir "Poscondiciones" → "Postcondiciones"
- Arreglar repeticiones en "Requerimientos"
- Agregar/completar justificaciones en Prioridad y Riesgo
- Mantener fielmente el formato de tabla de la plantilla oficial

## Archivos Referenciados

- `anexos/introduccion.md` — Fuente principal de información sobre el sistema, requisitos funcionales y no funcionales, y descripciones de los casos de uso.
- `diagramas/03-escenarios-casos-de-uso/PLANTILLA_ESCENARIO.md` — Plantilla oficial proporcionada por el docente con el formato exacto de tablas que se debía seguir.

## Ajustes Realizados al Output

- **Formato de tablas**: Se ajustó estrictamente al formato de la plantilla (tablas separadas para Nombre del escenario, Activar Evento, Tipo de señal, Pasos con "Información para los pasos", y tabla de Condiciones, suposiciones y preguntas).
- **Activar Evento**: Se mejoró la redacción para que fuera más clara y profesional.
- **Identificadores e iniciadores de caso de uso**: Se completó con un guion (`-`) para mantener la estructura de la tabla.
- **Pre y Postcondiciones**: Se ampliaron ligeramente para mayor completitud y precisión.
- **Requerimientos**: Se corrigió la repetición y se organizaron mejor (RF y RNF).
- **Prioridad y Riesgo**: Se agregaron justificaciones breves y coherentes.
- **General**: Se mantuvo el contenido realista basado en `introduccion.md`, sin inventar información.

Los 5 escenarios documentados son:
- CU-01: Agendar Turno
- CU-02: Registrar Llegada de Paciente
- CU-03: Gestionar Disponibilidad
- CU-04: Reprogramar Turno
- CU-05: Consultar Agenda

Todos los archivos se encuentran en: `diagramas/03-escenarios-casos-de-uso/`