# Anexos - Introducción al Diseño Orientado a Objetos
## Los cuatro fundamentos de POO
## Requisitos iniciales del sistema
## Casos de uso
### - Agendar Turno

**Nombre del caso de uso:** Agendar Turno.

**Actor(es) involucrado(s):** Secretaria.

**Descripción breve:** Permite a la secretaria asignar una cita a un paciente con un profesional específico, validando que el horario esté libre y que se cumplan las reglas de negocio (duración según tipo de consulta y restricciones horarias del médico).

**Flujo principal de eventos:**

* La secretaria selecciona la opción "Nuevo Turno" desde la vista de la agenda.

* El sistema solicita los datos del paciente (búsqueda por DNI o Nombre).

* La secretaria selecciona al Profesional y el Tipo de Consulta (Control o Primera Consulta).

* El sistema muestra un calendario con los huecos disponibles, filtrando automáticamente las restricciones (ej: bloquea los jueves por la tarde y no muestra "Primeras Consultas" los viernes a última hora).

* La secretaria selecciona una fecha y una hora de la lista de espacios disponibles (15 min para control, 30 min para primera consulta).

* La secretaria confirma la reserva del turno.

* El sistema verifica internamente que no haya ocurrido una superposición durante el proceso (validación de concurrencia).

* El sistema registra el turno con estado "Pendiente" y muestra un mensaje de confirmación exitosa.

**Precondiciones:**

* La secretaria debe estar autenticada en el sistema.

* El profesional debe estar registrado con sus horarios de atención base definidos.

* El paciente debe existir en el sistema (o el sistema debe permitir su creación rápida en el flujo).


**Postcondiciones:**

* El turno queda guardado en la base de datos vinculado al paciente y al profesional.

* El horario seleccionado queda marcado como "Ocupado" en la agenda, impidiendo nuevas reservas en ese bloque.

* Se genera de forma automática una tarea programada para el envío del recordatorio (WhatsApp/Email) el día anterior a la cita.


### - Registrar Llegada de Paciente

**Nombre del caso de uso:** Registrar Llegada de Paciente.

**Actor(es) involucrado(s):** Secretaria, Doctor

**Descripción breve:** El proceso permite registrar el momento exacto en que un paciente llega físicamente al consultorio para su cita. Esto cambia el estado del turno y permite al doctor saber desde su propia pantalla quién está ya en la sala de espera.

**Flujo principal de eventos:**

* El paciente se presenta en la recepción del consultorio.

* La secretaria busca al paciente en la lista de turnos del día.

* La secretaria selecciona la opción "Marcar Presente" o "Registrar Llegada" en el turno correspondiente.

* El sistema captura automáticamente la hora del servidor y la registra como Hora Real de Llegada.

* El sistema cambia el estado del turno de "Pendiente" a "Presente / En Sala".

* El sistema actualiza visualmente la agenda (ej. cambiando el color del turno o añadiendo un icono de tilde) para indicar que el paciente está esperando.

* El Doctor visualiza en su interfaz la actualización, confirmando que ya puede llamar al paciente.

**Precondiciones:**
* El paciente debe tener un turno previamente agendado para el día de la fecha.

* La secretaria debe tener abierta la vista de "Agenda Diaria" o "Monitor de Sala".

**Postcondiciones:**

* El estado del turno se actualiza en la base de datos de forma persistente.

* Queda registrado el dato de puntualidad (diferencia entre hora pactada y hora real de llegada) para fines estadísticos.

* El paciente queda disponible en la "cola de atención" del profesional.

### - Gestionar Disponibilidad

**Nombre del caso de uso:** Gestionar Disponibilidad.

**Actor(es) involucrado(s):** Profesional o Secretaria.

**Descripción breve:** Permite definir rangos horarios o días completos en los que el profesional no recibirá pacientes, ya sea por motivos recurrentes (clases, reuniones fijas), eventos únicos (vacaciones, feriados) o restricciones de tipo de práctica (no hacer procedimientos ciertos días).


**Flujo principal de eventos:**

* El usuario ingresa al módulo de "Configuración de Agenda" o hace clic derecho sobre un espacio vacío en la vista de calendario.

* El sistema solicita definir el Tipo de Bloqueo: Recurrente (ej: todos los jueves a la tarde por clases),Específico (ej: feriado puente o vacaciones),Restricción de actividad (ej: los lunes no se permiten "procedimientos").

* El usuario ingresa la fecha (o día de la semana), el rango horario y el motivo del bloqueo.

* El sistema verifica si ya existen turnos agendados en ese periodo,si hay conflictos, el sistema muestra una lista de los turnos afectados y solicita confirmación para proceder (indicando que esos turnos deberán ser reprogramados).

* El usuario confirma la operación.

* El sistema actualiza la base de datos de "Reglas de Disponibilidad".

* El sistema sombrea o deshabilita visualmente esos bloques en la agenda para que no se puedan seleccionar al crear nuevos turnos.

**Precondiciones:**

* El profesional debe estar registrado en el sistema.

* El usuario debe tener permisos para modificar la configuración de la agenda.

**Postcondiciones:**

* Cualquier intento posterior de agendar un turno en ese horario será rechazado por el sistema con un mensaje de "Horario no disponible".

* La vista de la secretaria refleja claramente el motivo del bloqueo (ej: "Clase Universidad" o "Feriado").


### - Reprogramar Turno

**Nombre del caso de uso:** Reprogramar Turno.

**Actor(es) involucrado(s):** Secretaria

**Descripción breve:** Permite cambiar la fecha y/o hora de un turno ya existente, liberando el espacio anterior y validando la disponibilidad del nuevo horario seleccionado, disparando una notificación automática al paciente.


**Flujo principal de eventos:**

* La secretaria busca el turno original en la agenda (por nombre de paciente o fecha).

* La secretaria selecciona la opción "Reprogramar".

* El sistema muestra el calendario de disponibilidad del profesional, manteniendo el tipo de consulta (Control o Primera) y su duración asociada.

* La secretaria selecciona la nueva fecha y hora disponible.

* El sistema solicita (opcionalmente) el motivo de la reprogramación para el registro interno.

* La secretaria confirma el cambio.

+ El sistema libera el bloque horario anterior, lo marca como "Disponible" y reserva el nuevo espacio con estado "Pendiente".

* El sistema genera y envía una notificación automática al paciente (vía WhatsApp o Email) con los nuevos datos de la cita.

**Precondiciones:**

* Debe existir un turno previo registrado en el sistema.

* El profesional debe tener disponibilidad en la nueva fecha/hora solicitada.


**Postcondiciones:**

* La agenda se actualiza reflejando el cambio.

* Se mantiene la trazabilidad del turno (el sistema registra que fue un turno movido y no uno nuevo desde cero).

* El paciente recibe la confirmación de la nueva fecha.




Consultar Agenda


## Boceto inicial de diseño de clases
