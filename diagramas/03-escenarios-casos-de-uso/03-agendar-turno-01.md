| **Nombre del escenario:** | Flujo principal - Agendar Turno | | | |
|---|---|---|---|---|
| **Nombre del caso de uso:** | Agendar Turno | | **ID Única:** | CU-01 |
| **Área** | Gestión de Turnos Médicos | | | |
| **Actor(es):** | Recepcionista | | | |
| **Descripción:** | Permite registrar un nuevo turno para un paciente con un profesional, validando disponibilidad, tipo de consulta y restricciones de agenda. | | | |

| **Activar Evento:** | La recepcionista hace clic en "Nuevo Turno" desde la vista de agenda para iniciar el proceso de reserva de una cita. | **Identificadores e iniciadores de caso de uso** |
|---|---|---|
| **Tipo de señal:** | ☑️ Externa | ☐ Temporal | |

| **Pasos desempeñados (ruta principal)** | **Información para los pasos** |
|---|---|
| 1. La recepcionista selecciona "Nuevo Turno" en la agenda. | La interfaz presenta el formulario de turno y la búsqueda de pacientes. |
| 2. El sistema solicita el paciente por DNI o nombre. | Si el paciente no existe, se permite crear uno nuevo con datos básicos. |
| 3. La recepcionista elige profesional y tipo de consulta. | Opciones: Control (15 min) o Primera Consulta (30 min). |
| 4. El sistema muestra los horarios disponibles. | Se filtran bloqueos, sobreturnos y reglas de disponibilidad del profesional. |
| 5. La recepcionista selecciona fecha y hora disponible. | El sistema calcula la duración y evita solapamientos. |
| 6. La recepcionista confirma la reserva. | El sistema valida nuevamente la disponibilidad en tiempo real. |
| 7. El sistema registra el turno con estado "Pendiente". | El turno queda asociado a paciente, profesional y tipo de consulta. |
| 8. El sistema programa recordatorio para el día anterior. | Se genera una tarea de notificación por WhatsApp/Email si está configurado. |

| **Condiciones, suposiciones y preguntas** | |
|---|---|
| **Precondiciones:** | Recepcionista autenticada; profesional con horarios configurados; paciente existente o creado en el flujo. |
| **Poscondiciones:** | Turno guardado; horario reservado; recordatorio programado. |
| **Suposiciones:** | Agenda y base de datos disponibles; reglas de duración y restricciones definidas; la recepción tiene conexión estable. |
| **Requerimientos:** | RF1: Gestión de Turnos; RF1: Control de Conflictos; RNF1: Usabilidad; RNF1: Integridad de Datos. |
| **Aspectos sobresalientes:** | Validación en tiempo real de disponibilidad; filtrado automático de bloqueos; creación de paciente en el mismo flujo. |
| **Prioridad:** | Alta - Porque es la funcionalidad principal del sistema de turnos. |
| **Riesgo:** | Medio - Porque la concurrencia y la disponibilidad deben manejarse correctamente. |