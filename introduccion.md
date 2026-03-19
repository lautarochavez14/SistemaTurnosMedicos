# Anexos - Introducción al Diseño Orientado a Objetos
## Los cuatro fundamentos de POO
## Requisitos iniciales del sistema

[NotebookLM](https://notebooklm.google.com/notebook/c6fb2197-0990-4141-9561-90868718a7fb)

**Requisitos Funcionales (RF1):**

* Gestión de Turnos:

  * Crear, reprogramar y cancelar turnos de manera digital.
 
  * Diferenciar entre tipos de consulta (control o primera vez) para estimar la duración (15 o 30 minutos).
 
  * Permitir que el paciente notifique una cancelación, la cual debe quedar registrada.

* Gestión de la Agenda:

  * Visualizar la agenda por profesional de forma diaria y semanal.
 
  * Bloquear horarios por vacaciones, feriados, reuniones o actividades fijas del profesional (como clases los jueves).
 
  * Manejar la disponibilidad base del profesional y excepciones (como guardias matutinas variables).

* Control de Conflictos y Sobreturnos:

  * Evitar la superposición de turnos (doble reserva) de forma automática.
 
  * Permitir el agregado manual de sobreturnos (máximo dos por día), solo bajo autorización del profesional.

* Seguimiento de Pacientes en Sala:

  * Registrar la llegada física del paciente al consultorio (marcar como "presente").
 
  * Registrar, de ser posible, la hora real de llegada para compararla con el turno programado.

* Notificaciones y Alertas:

  * Enviar recordatorios automáticos el día anterior (preferentemente vía WhatsApp).
 
  * Notificar automáticamente cambios o cancelaciones a los pacientes.

* Auditoría y Registro:

  * Mantener un historial de cambios de turno para resolver disputas sobre quién realizó modificaciones.
 
  * Modelar conceptualmente una lista de espera para cubrir lugares que se liberen.

**Requisitos No Funcionales (RNF1):**

* Usabilidad: El sistema debe tener una interfaz simple y fácil de usar, especialmente para el médico, evitando procesos de aprendizaje complejos.

* Escabilidad/Extensibilidad: El diseño inicial debe ser extensible para permitir la incorporación de más profesionales y salas en el futuro, aunque el MVP sea para uno solo.

* Integridad de Datos: El modelo debe asegurar el encapsulamiento, impidiendo que se manipule la lista de turnos sin pasar por la lógica de verificación de disponibilidad de la agenda.

* Oportunidad (Time-To-Market): El Producto Mínimo Viable (MVP) debe estar funcional para principios de julio.

* Prioridad de Modelo sobre Diseño: En la fase inicial, se busca la corrección del modelo de dominio y su funcionamiento lógico antes que un diseño visual perfecto.

* Mantenibilidad: Se requiere un diseño basado en un dominio claro (clases y responsabilidades bien definidas) para facilitar iteraciones futuras sin "parches".
## Casos de uso
## Boceto inicial de diseño de clases
