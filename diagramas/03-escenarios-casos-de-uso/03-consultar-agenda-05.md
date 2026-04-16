| **Nombre del escenario:** | Flujo principal - Consultar Agenda | | | |
|---|---|---|---|---|
| **Nombre del caso de uso:** | Consultar Agenda | | **ID Única:** | CU-05 |
| **Área** | Gestión de Turnos Médicos | | | |
| **Actor(es):** | Recepcionista, Profesional | | | |
| **Descripción:** | Permite visualizar turnos, bloqueos y sobreturnos en vistas diaria, semanal o mensual. | | | |

| **Activar Evento:** | El usuario abre la sección "Agenda" desde el menú principal para consultar la programación del profesional. | - |
|---|---|---|
| **Tipo de señal:** | ☑️ Externa | ☐ Temporal | |

| **Pasos desempeñados (ruta principal)** | **Información para los pasos** |
|---|---|
| 1. El usuario accede a la sección "Agenda". | Desde el menú principal del sistema. |
| 2. El sistema muestra la vista diaria por defecto. | Para el profesional seleccionado y día actual. |
| 3. El usuario selecciona vista (Día, Semana, Mes). | Utiliza controles de navegación. |
| 4. El sistema recupera y presenta los eventos. | Turnos, bloqueos, sobreturnos con códigos de colores. |
| 5. El usuario navega por fechas. | Utiliza selector de calendario. |
| 6. Al posicionar el cursor, muestra vista rápida. | Detalles de paciente y observaciones. |

| **Condiciones, suposiciones y preguntas** | |
|---|---|
| **Precondiciones:** | Usuario autenticado; datos de agenda disponibles en la base de datos. |
| **Postcondiciones:** | Visualización de disponibilidad y ocupación; identificación de pacientes presentes. |
| **Suposiciones:** | Datos actualizados en tiempo real; interfaz responsiva; filtros por profesional. |
| **Requerimientos:** | RF1: Gestión de la Agenda; RNF1: Usabilidad; RNF2: Escalabilidad. |
| **Aspectos sobresalientes:** | Códigos de colores intuitivos; navegación flexible; vista rápida de detalles. |
| **Prioridad:** | Alta - Es fundamental para que el personal pueda monitorear la agenda y tomar decisiones operativas. |
| **Riesgo:** | Bajo - Se trata de una acción de consulta con mínimo impacto en el sistema. |