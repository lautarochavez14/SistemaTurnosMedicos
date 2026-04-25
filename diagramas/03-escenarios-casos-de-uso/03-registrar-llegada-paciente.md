| **Nombre del escenario:** | Flujo principal - Registrar Llegada de Paciente | | | |
|---|---|---|---|---|
| **Nombre del caso de uso:** | Registrar Llegada de Paciente | | **ID Única:** | CU-02 |
| **Área** | Gestión de Turnos Médicos | | | |
| **Actor(es):** | Recepcionista, Profesional | | | |
| **Descripción:** | Registra la llegada física del paciente al consultorio, actualizando el estado del turno y permitiendo al profesional visualizar la cola de atención. | | | |

| **Activar Evento:** | El paciente llega físicamente a recepción, y la recepcionista inicia el proceso de registro de llegada desde la vista de agenda. | **Identificadores e iniciadores de caso de uso** |
|---|---|---|
| **Tipo de señal:** | ☑️ Externa | ☐ Temporal | |

| **Pasos desempeñados (ruta principal)** | **Información para los pasos** |
|---|---|
| 1. El paciente llega a recepción. | El paciente presenta su identificación o es reconocido por la recepcionista. |
| 2. La recepcionista busca el turno en la lista del día. | Utiliza filtros por nombre de paciente o fecha. |
| 3. La recepcionista selecciona "Marcar Presente" en el turno. | La interfaz muestra el turno correspondiente. |
| 4. El sistema captura la hora real de llegada. | Utiliza el reloj del servidor para registrar el timestamp. |
| 5. El sistema cambia el estado del turno a "Presente". | Actualiza el estado en la base de datos. |
| 6. El sistema actualiza la vista de agenda visualmente. | Cambia colores o iconos para indicar presencia. |
| 7. El profesional visualiza la actualización en su interfaz. | Permite llamar al paciente desde la cola de atención. |

| **Condiciones, suposiciones y preguntas** | |
|---|---|
| **Precondiciones:** | El paciente debe tener un turno previamente agendado para la fecha actual; la recepcionista debe tener acceso a la vista de agenda diaria. |
| **Postcondiciones:** | El estado del turno se actualiza a 'Presente'; se registra la hora real de llegada para estadísticas de puntualidad; el paciente queda disponible en la cola de atención del profesional. |
| **Suposiciones:** | Reloj del servidor preciso; base de datos accesible; interfaz en tiempo real. |
| **Requerimientos:** | RF1: Seguimiento de Pacientes en Sala; RNF1: Usabilidad; RNF1: Integridad de Datos. |
| **Aspectos sobresalientes:** | Actualización en tiempo real; registro automático de hora; visualización para múltiples usuarios. |
| **Prioridad:** | Alta - Porque permite el flujo eficiente de pacientes en el consultorio. |
| **Riesgo:** | Bajo - Porque es un proceso de actualización simple sin cálculos complejos. |