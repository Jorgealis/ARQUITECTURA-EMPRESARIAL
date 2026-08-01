# Desarrollo

1. Identifique los actores del proceso (¿quién participa? ¿qué rol cumple cada uno?).

   Se identificaron como actores del proceso Paciente y el Sistema de Agendamiento de la Clínica. El paciente cumple el rol de solicitante, quien inicia la transacción con el sistema para agendar su cita y el sistema se encarga de procesar esta solicitud, comprobando disponibilidad y guardando la cita en la base de datos.

2. Defina el evento de inicio y los posibles eventos de fin.

   Inicio: 

   - El paciente ingresa a la sección de agendamiento de citas de la plataforma de la clínica.

   Fin: 

   - No se pudo agendar por falta de disponibilidad. 

   - Se pudo agendar la cita correctamente.

     Para ambos casos se envía mensaje para informar el caso via correo o mensaje de texto.

3. Liste las actividades principales de cada actor.

   Paciente

   - Ingresa datos de información personal contacto

   - Selección de especialidad

   - Selección de fecha

   - Enviar datos al sistema

   - Revisión de mensaje de confirmación

   Sistema

   - Guardar datos
   - Comprobar disponibilidad del médico
   - Enviar confirmación de agendamiento de cita correctamente
   - Enviar confirmación de falta de disponibilidad

4. Inserte los gateways (decisiones) y formule su pregunta.

   - ¿Hay disponibilidad?
   - ¿El usuario existe?

5. Conecte todo con flujos de secuencia, etiquete las salidas de cada gateway y valide el modelo con la [checklist de autoevaluación](https://github.com/Jorgealis/ARQUITECTURA-EMPRESARIAL/blob/main/clase/guia_paso_a_paso_bpmn.md#5-checklist-de-autoevaluación-antes-de-entregar).

- Use papel, pizarra o herramientas como draw.io o Camunda Modeler.
- Reciba retroalimentación del docente y registre avances en `clase/notas.md` (use la [plantilla de notas](https://github.com/Jorgealis/ARQUITECTURA-EMPRESARIAL/blob/main/plantillas/plantilla_notas.md)).
