| **Nombre del escenario:** | Flujo principal - Gestionar Disponibilidad | | | |
|---|---|---|---|---|
| **Nombre del caso de uso:** | Gestionar Disponibilidad | | **ID Única:** | CU-03 |
| **Área** | Gestión de Turnos Médicos | | | |
| **Actor(es):** | Profesional, Recepcionista | | | |
| **Descripción:** | Permite definir bloqueos horarios en la agenda por motivos recurrentes o únicos, evitando reservas en esos periodos. | | | |

| **Activar Evento:** | El usuario (profesional o recepcionista) accede al módulo de configuración de agenda para crear un bloqueo horario. | - |
|---|---|---|
| **Tipo de señal:** | ☑️ Externa | ☐ Temporal | |

| **Pasos desempeñados (ruta principal)** | **Información para los pasos** |
|---|---|
| 1. El usuario ingresa al módulo de "Configuración de Agenda". | Selecciona desde el menú principal o hace clic derecho en el calendario. |
| 2. El sistema solicita definir el tipo de bloqueo. | Opciones: Recurrente, Específico o Restricción de actividad. |
| 3. El usuario ingresa fecha, rango horario y motivo. | Utiliza calendario y campos de texto para detalles. |
| 4. El sistema verifica conflictos con turnos existentes. | Muestra lista de turnos afectados si los hay. |
| 5. El usuario confirma la operación. | Requiere aceptación si hay reprogramaciones necesarias. |
| 6. El sistema actualiza las reglas de disponibilidad. | Guarda en base de datos las restricciones. |
| 7. El sistema sombrea los bloques en la agenda. | Actualiza la vista visual para impedir selecciones. |

| **Condiciones, suposiciones y preguntas** | |
|---|---|
| **Precondiciones:** | El profesional debe estar registrado en el sistema; el usuario debe tener permisos de modificación de agenda; debe existir al menos un horario base configurado. |
| **Postcondiciones:** | Los horarios bloqueados quedan persistentes en la base de datos; todos los intentos de agendamiento en esos periodos son rechazados automáticamente; la vista de agenda refleja visualmente los bloques. |
| **Suposiciones:** | Base de datos persistente; reglas aplicadas automáticamente; notificaciones de conflictos. |
| **Requerimientos:** | RF1: Gestión de la Agenda; RNF1: Mantenibilidad; RNF2: Integridad de Datos. |
| **Aspectos sobresalientes:** | Soporte para bloqueos recurrentes; verificación de conflictos; actualización visual inmediata. |
| **Prioridad:** | Media - Funcionalidad administrativa importante pero no crítica para la operación diaria del consultorio. |
| **Riesgo:** | Medio - Posible impacto en la disponibilidad de turnos y potencial necesidad de reprogramaciones de citas existentes. |