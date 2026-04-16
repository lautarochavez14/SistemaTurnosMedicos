| **Nombre del escenario:** | Flujo principal - Reprogramar Turno | | | |
|---|---|---|---|---|
| **Nombre del caso de uso:** | Reprogramar Turno | | **ID Única:** | CU-04 |
| **Área** | Gestión de Turnos Médicos | | | |
| **Actor(es):** | Recepcionista | | | |
| **Descripción:** | Permite cambiar la fecha y hora de un turno existente, liberando el horario anterior y validando el nuevo. | | | |

| **Activar Evento:** | La recepcionista inicia la acción de reprogramar un turno desde la agenda para cambiar la fecha y hora de una cita existente. | - |
|---|---|---|
| **Tipo de señal:** | ☑️ Externa | ☐ Temporal | |

| **Pasos desempeñados (ruta principal)** | **Información para los pasos** |
|---|---|
| 1. La recepcionista busca y selecciona el turno original. | Utiliza filtros por paciente o fecha. |
| 2. La recepcionista elige "Reprogramar". | Abre el formulario de modificación. |
| 3. El sistema muestra el calendario de disponibilidad. | Mantiene tipo de consulta y duración. |
| 4. La recepcionista selecciona nueva fecha y hora. | El sistema valida disponibilidad. |
| 5. La recepcionista ingresa motivo opcional. | Campo de texto para registro interno. |
| 6. La recepcionista confirma el cambio. | El sistema verifica nuevamente. |
| 7. El sistema libera el horario anterior y reserva el nuevo. | Actualiza estados y asociaciones. |
| 8. El sistema envía notificación al paciente. | Programada por WhatsApp/Email. |

| **Condiciones, suposiciones y preguntas** | |
|---|---|
| **Precondiciones:** | Turno existente registrado; profesional con disponibilidad en nueva fecha. |
| **Postcondiciones:** | Agenda actualizada; trazabilidad mantenida; paciente notificado. |
| **Suposiciones:** | Comunicación efectiva con el paciente; base de datos consistente; notificaciones configuradas. |
| **Requerimientos:** | RF1: Gestión de Turnos; RF2: Notificaciones; RNF1: Oportunidad. |
| **Aspectos sobresalientes:** | Liberación automática de horarios; notificaciones automáticas; mantenimiento de historial. |
| **Prioridad:** | Alta - Porque habilita la modificación de turnos existentes y mantiene la continuidad del servicio. |
| **Riesgo:** | Medio - Porque involucra cambios en la disponibilidad y notificaciones que deben procesarse correctamente. |