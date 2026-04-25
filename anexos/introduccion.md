# Anexos - Introducción al Diseño Orientado a Objetos
- ¿Qué es el Paradigma Orientado a Objetos (POO)?

El Paradigma Orientado a Objetos (POO) es un paradigma basado en la organización del código en objetos, que representan entidades del mundo real.
Es importante porque permite crear software modular, reutilizable y fácil de mantener.


## Los cuatro fundamentos de POO

- Abstracción:
  
Es la capacidad de representar elementos del mundo real en el código mediante la división entre distintos elementos más sencillos de entender, como los atributos que lo componen y los procedimientos que puede realizar.
Ejemplo: La entidad "Turno" tiene distintos atributos, como fecha, hora, estado, etc.

- Encapsulamiento:
  
Protege los datos de un objeto, permitiendo acceso solo a través de métodos específicos.
Ejemplo: La entidad "Turno" protege sus datos y solo permite la posibilidad de aprobar sobreturnos por parte de la entidad "Médico".

- Herencia:
  
Permite que una clase reutilice características de otra.
Ejemplo: "Médico" y "Paciente" heredan de la clase "Persona" al tener ambos atributos como nombre, dni y teléfono.


- Polimorfismo:

Permite que una misma acción tenga diferentes comportamientos según el objeto.
Ejemplo: El procedimiento notificar() se comporta diferente si lo invoca un "Paciente" (WhatsApp) a que lo invoque el propio sistema (registro interno de auditoría).


## Link al NotebookLM

[NotebookLM](https://notebooklm.google.com/notebook/c6fb2197-0990-4141-9561-90868718a7fb)


## Requisitos iniciales del sistema


**Requisitos Funcionales:**

**RF1 - Gestión de Turnos:** El sistema debe permitir crear, reprogramar y cancelar turnos de manera digital, diferenciar entre tipos de consulta (control o primera vez) para estimar la duración (15 o 30 minutos) y permitir que el paciente notifique una cancelación, la cual debe quedar registrada.

**RF2 - Gestión de la Agenda:** El sistema debe permitir visualizar la agenda por profesional de forma diaria y semanal, bloquear horarios por vacaciones, feriados, reuniones o actividades fijas del profesional (como clases los jueves) y manejar la disponibilidad base del profesional y excepciones (como guardias matutinas variables).

**RF3 - Control de Conflictos y Sobreturnos:** El sistema debe impedir la superposición de turnos (doble reserva) de forma automática y permitir el agregado manual de sobreturnos (máximo dos por día), solo bajo autorización del profesional.

**RF4 - Seguimiento de Pacientes en Sala:** El sistema debe registrar la llegada física del paciente al consultorio (marcar como "presente") y, de ser posible, la hora real de llegada para compararla con el turno programado.

**RF5 - Notificaciones y Alertas:** El sistema debe enviar recordatorios automáticos el día anterior (preferentemente vía WhatsApp), al mismo tiempo que debe de notificar automáticamente cambios o cancelaciones a los pacientes.

**RF6 - Auditoría y Registro:** El sistema debe mantener un historial de cambios de turno para resolver disputas sobre quién realizó modificaciones y modelar conceptualmente una lista de espera para cubrir lugares que se liberen.

**Requisitos No Funcionales:**

**RNF1 - Usabilidad:** El sistema debe tener una interfaz simple y fácil de usar, especialmente para el médico, evitando procesos de aprendizaje complejos.

**RNF2 - Escabilidad/Extensibilidad:** El diseño inicial debe ser extensible para permitir la incorporación de más profesionales y salas en el futuro, aunque el MVP sea para uno solo.

**RNF3 - Integridad de Datos:** El modelo debe asegurar el encapsulamiento, impidiendo que se manipule la lista de turnos sin pasar por la lógica de verificación de disponibilidad de la agenda.

**RNF4 - Oportunidad (Time-To-Market):** El Producto Mínimo Viable (MVP) debe estar funcional para principios de julio.

**RNF5 - Prioridad de Modelo sobre Diseño:** En la fase inicial, se busca la corrección del modelo de dominio y su funcionamiento lógico antes que un diseño visual perfecto.

**RNF6 - Mantenibilidad:** Se requiere un diseño basado en un dominio claro (clases y responsabilidades bien definidas) para facilitar iteraciones futuras sin "parches".


## Casos de uso



### - Agendar Turno

**Nombre del caso de uso:** Agendar Turno.

**Actor(es) involucrado(s):** Recepcionista.

**Descripción breve:** Permite a la Recepcionista asignar una cita a un paciente con un profesional específico, validando que el horario esté libre y que se cumplan las reglas de negocio (duración según tipo de consulta y restricciones horarias del médico).

**Flujo principal de eventos:**

* La Recepcionista selecciona la opción "Nuevo Turno" desde la vista de la agenda.

* El sistema solicita los datos del paciente (búsqueda por DNI o Nombre).

* La Recepcionista selecciona al Profesional y el Tipo de Consulta (Control o Primera Consulta).

* El sistema muestra un calendario con los huecos disponibles, filtrando automáticamente las restricciones (ej: bloquea los jueves por la tarde y no muestra "Primeras Consultas" los viernes a última hora).

* La Recepcionista selecciona una fecha y una hora de la lista de espacios disponibles (15 min para control, 30 min para primera consulta).

* La Recepcionista confirma la reserva del turno.

* El sistema verifica internamente que no haya ocurrido una superposición durante el proceso (validación de concurrencia).

* El sistema registra el turno con estado "Pendiente" y muestra un mensaje de confirmación exitosa.

**Precondiciones:**

* La Recepcionista debe estar autenticada en el sistema.

* El profesional debe estar registrado con sus horarios de atención base definidos.

* El paciente debe existir en el sistema (o el sistema debe permitir su creación rápida en el flujo).


**Postcondiciones:**

* El turno queda guardado en la base de datos vinculado al paciente y al profesional.

* El horario seleccionado queda marcado como "Ocupado" en la agenda, impidiendo nuevas reservas en ese bloque.

* Se genera de forma automática una tarea programada para el envío del recordatorio (WhatsApp/Email) el día anterior a la cita.




### - Registrar Llegada de Paciente

**Nombre del caso de uso:** Registrar Llegada de Paciente.

**Actor(es) involucrado(s):** Recepcionista,Profesional

**Descripción breve:** El proceso permite registrar el momento exacto en que un paciente llega físicamente al consultorio para su cita. Esto cambia el estado del turno y permite al doctor saber desde su propia pantalla quién está ya en la sala de espera.

**Flujo principal de eventos:**

* El paciente se presenta en la recepción del consultorio.

* La Recepcionista busca al paciente en la lista de turnos del día.

* La Recepcionista selecciona la opción "Marcar Presente" o "Registrar Llegada" en el turno correspondiente.

* El sistema captura automáticamente la hora del servidor y la registra como Hora Real de Llegada.

* El sistema cambia el estado del turno de "Pendiente" a "Presente / En Sala".

* El sistema actualiza visualmente la agenda (ej. cambiando el color del turno o añadiendo un icono de tilde) para indicar que el paciente está esperando.

* El Doctor visualiza en su interfaz la actualización, confirmando que ya puede llamar al paciente.

**Precondiciones:**
* El paciente debe tener un turno previamente agendado para el día de la fecha.

* La Recepcionista debe tener abierta la vista de "Agenda Diaria" o "Monitor de Sala".

**Postcondiciones:**

* El estado del turno se actualiza en la base de datos de forma persistente.

* Queda registrado el dato de puntualidad (diferencia entre hora pactada y hora real de llegada) para fines estadísticos.

* El paciente queda disponible en la "cola de atención" del profesional.




### - Gestionar Disponibilidad

**Nombre del caso de uso:** Gestionar Disponibilidad.

**Actor(es) involucrado(s):** Profesional o Recepcionista

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

* La vista de la Recepcionista refleja claramente el motivo del bloqueo (ej: "Clase Universidad" o "Feriado").



### - Reprogramar Turno

**Nombre del caso de uso:** Reprogramar Turno.

**Actor(es) involucrado(s):** Recepcionista

**Descripción breve:** Permite cambiar la fecha y/o hora de un turno ya existente, liberando el espacio anterior y validando la disponibilidad del nuevo horario seleccionado, disparando una notificación automática al paciente.


**Flujo principal de eventos:**

* La Recepcionista busca el turno original en la agenda (por nombre de paciente o fecha).

* La Recepcionista selecciona la opción "Reprogramar".

* El sistema muestra el calendario de disponibilidad del profesional, manteniendo el tipo de consulta (Control o Primera) y su duración asociada.

* La Recepcionista selecciona la nueva fecha y hora disponible.

* El sistema solicita (opcionalmente) el motivo de la reprogramación para el registro interno.

* La Recepcionista confirma el cambio.

+ El sistema libera el bloque horario anterior, lo marca como "Disponible" y reserva el nuevo espacio con estado "Pendiente".

* El sistema genera y envía una notificación automática al paciente (vía WhatsApp o Email) con los nuevos datos de la cita.

**Precondiciones:**

* Debe existir un turno previo registrado en el sistema.

* El profesional debe tener disponibilidad en la nueva fecha/hora solicitada.


**Postcondiciones:**

* La agenda se actualiza reflejando el cambio.

* Se mantiene la trazabilidad del turno (el sistema registra que fue un turno movido y no uno nuevo desde cero).

* El paciente recibe la confirmación de la nueva fecha.





### - Consultar Agenda

**Nombre del caso de uso:** Consultar Agenda.

**Actor(es) involucrado(s):** Recepcionista,Profesional

**Descripción breve:** Permite visualizar de forma organizada y clara los turnos programados, los sobreturnos y los espacios bloqueados de un profesional en un período determinado (día o semana), reflejando el estado en tiempo real de cada cita.

**Flujo principal de eventos:**

* El usuario accede a la sección "Agenda" del menú principal.

* El sistema muestra por defecto la vista Diaria del día actual para el profesional seleccionado.

* El usuario selecciona entre la vista "Día", "Semana" o "Mes" según su necesidad.

* El sistema recupera y presenta cronológicamente todos los eventos del período:Turnos (con nombre de paciente y tipo de consulta),Bloqueos (clases, feriados, reuniones).,Sobreturnos autorizados.

* El sistema aplica un código de colores o iconos para identificar el Estado del Turno (Pendiente, Presente en sala, Cancelado o Atendido).

* El usuario utiliza el selector de fecha (mini calendario) para navegar hacia adelante o atrás en el tiempo,al posicionar el cursor sobre un turno, el sistema despliega una "vista rápida" con datos de contacto del paciente y observaciones, sin necesidad de cambiar de pantalla.

**Precondiciones:**

* El usuario debe estar autenticado en el sistema.

* Deben existir turnos, sobreturnos o bloqueos cargados en la base de datos para el profesional seleccionado.


**Postcondiciones:**

* El usuario visualiza la disponibilidad y ocupación real.

* El Profesional identifica rápidamente quiénes ya están físicamente en el consultorio (gracias al estado "Presente" derivado del Check-in).


## Boceto inicial de diseño de clases
![Boceto inicial](/diagramas/01-diagrama-clases/01-boceto-inicial.png)
