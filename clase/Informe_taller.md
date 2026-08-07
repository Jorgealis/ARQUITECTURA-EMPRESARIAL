# 📄 Informe Técnico del Taller

## 🔖 Nombre del Taller
_Taller X - Modelado del Proceso de Agendamiento de Citas Médicas mediante BPMN_

## 👥 Integrantes del equipo
- Brayan Presiga
- Julian Aguirre
- Jorge Alarcon

## 🧠 Descripción general del trabajo
El objetivo del taller consistió en modelar, mediante notación BPMN (Business Process Model and Notation), el proceso de agendamiento de citas médicas de una plataforma en línea. La actividad se desarrolló identificando los actores involucrados en el proceso (el paciente y el sistema de agendamiento), las tareas que cada uno ejecuta, y los puntos de decisión que determinan el flujo alterno del proceso ante la disponibilidad o no disponibilidad del médico solicitado. A partir de este análisis se construyó un diagrama de swimlanes (carriles) que representa de forma clara la interacción entre el actor humano y el sistema.

## 🔧 Proceso de desarrollo
Para el desarrollo del taller, el equipo inició por identificar los dos actores principales del proceso: el Paciente, quien interactúa directamente con la plataforma, y el Sistema de Agendamiento, encargado de la lógica de negocio y el acceso a los datos. Se definieron dos carriles (lanes) dentro de un mismo pool llamado "Agendamiento de Citas Médicas", separando así las responsabilidades de cada actor.

Posteriormente se modeló el flujo principal: el evento de inicio en el que el paciente ingresa al área de citas, seguido de la tarea de selección de especialidad y fecha. A continuación, se representó la tarea del sistema para comprobar la disponibilidad del médico y se incorporó una compuerta exclusiva (gateway XOR) que evalúa la condición "¿Hay disponibilidad?". Se modelaron los dos caminos posibles: en caso negativo, el sistema notifica la falta de disponibilidad y el flujo retorna a la tarea de selección de especialidad y fecha, permitiendo al paciente intentar nuevamente; en caso afirmativo, el sistema guarda la información en la base de datos, notifica el agendamiento exitoso y el proceso finaliza en el evento de fin.

Como herramienta de modelado se utilizó un editor de diagramas BPMN (tipo drawio/BPMN.io), ajustando de manera iterativa la disposición de los elementos, la dirección de las flechas de secuencia y la redacción de las etiquetas de cada actividad, hasta lograr una representación clara y coherente del proceso de negocio.

## 🧩 Análisis del modelo propuesto
Incluya un análisis sobre:

**Cómo se estructura el modelo entregado**

El modelo se estructura como un diagrama de colaboración BPMN de un único pool ("Agendamiento de Citas Médicas") dividido en dos carriles: Paciente y Sistema de agendamiento. El flujo de secuencia es lineal con un único punto de decisión (gateway exclusivo), lo que genera un ciclo de reintento cuando no hay disponibilidad. El proceso cuenta con un evento de inicio (círculo verde) y un evento de fin (círculo rojo), cumpliendo con las reglas básicas de bien formado de BPMN: todo proceso debe iniciar y terminar con un evento explícito.

**Cómo representa las necesidades del cliente**

El diagrama responde a la necesidad del cliente de automatizar y agilizar el agendamiento de citas médicas, evitando que el paciente deba comunicarse telefónicamente o de forma presencial. El modelo deja explícito el punto crítico del negocio (la validación de disponibilidad del médico) y contempla el camino alterno de error o rechazo, lo cual es fundamental para que la experiencia del usuario no termine en un callejón sin salida: si no hay disponibilidad, el paciente puede intentar con otra especialidad o fecha sin salir del proceso.

**Qué supuestos se tomaron**

- Se asume que el paciente ya se encuentra autenticado en la plataforma antes de ingresar al módulo de citas.
- Se asume que la validación de disponibilidad es instantánea y no requiere intervención manual de un operador humano.
- No se modelan manejo de errores técnicos (caídas del sistema, fallos de conexión) ni casos de cancelación o reprogramación de citas, dado que el alcance del taller se limitó al flujo feliz y a un único camino alterno de "no disponibilidad".
- Se asume una única base de datos compartida entre las tareas de "comprobar disponibilidad" y "guardar información", sin representar explícitamente el almacén de datos como objeto de datos BPMN.

## 📈 Diagrama final entregado
> (Inserte aquí una imagen o enlace al modelo-final.drawio / .asta / PDF)

![Diagrama BPMN del proceso de agendamiento de citas médicas](diagrama.png)

*Figura 1. Diagrama BPMN del proceso de agendamiento de citas médicas (carriles: Paciente / Sistema de agendamiento).*

## 📋 Tabla de actores, entidades o componentes (si aplica)
| Nombre del elemento | Tipo | Descripción | Responsable |
|---------------------|------|-------------|-------------|
| Paciente | Actor / Rol (Lane) | Usuario que ingresa a la plataforma, selecciona especialidad y fecha para agendar una cita médica. | Cliente |
| Sistema de agendamiento | Actor / Rol (Lane) | Componente de software encargado de validar la disponibilidad del médico, registrar la cita y notificar el resultado. | Cliente |
| Ingresa al área de citas en la plataforma | Evento de inicio | Punto de partida del proceso: el paciente accede al módulo de agendamiento. | Paciente |
| Selección de la especialidad y la fecha | Tarea (Task) | El paciente elige la especialidad médica requerida y la fecha deseada para la cita. | Paciente |
| Comprobar disponibilidad del médico | Tarea (Task) | El sistema valida en la base de datos si existe disponibilidad para la especialidad y fecha solicitadas. | Sistema de agendamiento |
| ¿Hay disponibilidad? | Compuerta exclusiva (Gateway XOR) | Punto de decisión que determina si el flujo continúa hacia el registro de la cita o regresa al paciente. | Sistema de agendamiento |
| Notificar que no hay disponibilidad | Tarea (Task) | Si no hay disponibilidad, el sistema informa al paciente y lo redirige a elegir nuevamente especialidad y fecha. | Sistema de agendamiento |
| Guardar información en base de datos | Tarea (Task) | Si hay disponibilidad, el sistema persiste los datos de la cita agendada. | Sistema de agendamiento |
| Notificar agendamiento exitoso | Tarea (Task) | El sistema confirma al paciente que la cita fue agendada correctamente. | Sistema de agendamiento |
| Fin: Agendamiento Exitoso | Evento de fin | Cierre del proceso una vez confirmada la cita. | Sistema de agendamiento |

## 🔍 Investigación complementaria

### Tema investigado:
Buenas prácticas en el modelado de procesos con notación BPMN (Business Process Model and Notation).

### Resumen:
BPMN es un estándar gráfico mantenido por el Object Management Group (OMG) para la representación de procesos de negocio, cuyo propósito es ofrecer una notación comprensible tanto para analistas de negocio como para desarrolladores técnicos, facilitando la trazabilidad entre el diseño del proceso y su eventual implementación (por ejemplo, mediante motores de orquestación BPEL). Entre las buenas prácticas más relevantes se destacan: mantener un único evento de inicio y al menos un evento de fin claramente etiquetado, evitar cruces innecesarios de flujos de secuencia entre carriles, nombrar las tareas con estructura "verbo + objeto" (por ejemplo, "Comprobar disponibilidad") y utilizar compuertas (gateways) únicamente cuando existan condiciones de decisión reales, evitando su uso implícito.

En el caso del diagrama desarrollado en este taller, se aplicaron estas prácticas mediante el uso de carriles (lanes) para separar claramente las responsabilidades del paciente y del sistema, así como una compuerta exclusiva (XOR) explícita para representar la condición "¿Hay disponibilidad?". Asimismo, se procuró que cada tarea tuviera una única responsabilidad y un nombre descriptivo, siguiendo la recomendación de mantener la granularidad de las actividades a un nivel que sea comprensible sin necesidad de subprocesos adicionales.

Finalmente, la investigación permitió identificar que un aspecto frecuentemente recomendado —y que representa una oportunidad de mejora para el modelo entregado— es la incorporación de objetos de datos (Data Objects) y almacenes de datos (Data Stores) para representar explícitamente la base de datos consultada y actualizada por el sistema, así como el uso de eventos intermedios de mensaje para modelar de forma más precisa las notificaciones enviadas al paciente.

## 📚 Referencias
- [1] Object Management Group (OMG). *Business Process Model and Notation (BPMN), Version 2.0*. 2011. Disponible en: https://www.omg.org/spec/BPMN/
- [2] Fuente oficial BPMN: https://www.omg.org/spec/BPMN/

---
_Este documento hace parte de la entrega del taller X del curso AREM (Arquitectura Empresarial) - Universidad de La Sabana._
