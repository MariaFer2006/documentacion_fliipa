#### HU-019: Contacto simultáneo multicanal

| Campo | Detalle |
|:---:|:---:|
| **Actor** | Asesor comercial |
| **Historia** | Como asesor comercial, quiero contactar simultáneamente por correo, WhatsApp y llamada a los clientes preaprobados, para maximizar la tasa de respuesta. |
| **Prioridad** | Alta |
| **Precondiciones** | El asesor cuenta con la base de clientes preaprobados y con las plantillas de contacto por los tres canales. |
| **Criterios de aceptación** | El cliente recibe contacto por todos los canales definidos (correo, WhatsApp y llamada) y el equipo comercial puede registrar y consultar la tasa de respuesta por canal. |
| **Relaciones** | Casos de uso: CU-001. Requerimiento: RF-001. Historia relacionada: HU-001. |
| **Referencias** | [Procesos](../negocio/procesos/01-captacion-comercial.md); `b2b/services/rules-engine/src/db/repositories/get-clients.ts` |
| **Autor / Fecha / Versión** | María Fernanda Herazo |
| **Comentarios** | **Corrección v1.6**: el criterio de aceptación original ("El asesor cuenta con la base de clientes preaprobados y las plantillas de contacto por los tres canales") era en realidad una precondición (algo que se necesita para que la historia se cumpla), no un criterio de aceptación (cómo se sabe que la historia se cumple correctamente). Se traslada al nuevo campo "Precondiciones" y se reemplaza el criterio de aceptación por uno centrado en el resultado. Se revisaron los criterios de aceptación de todas las demás historias del documento y no se identificaron otros casos de precondiciones redactadas como criterios de aceptación. Existe una base de clientes preaprobados en `rules-engine` (`get-clients.ts`, `get-evaluation-clients.handler.ts`), pero no se encontró una herramienta de contacto multicanal orquestada para el asesor (llamadas, plantillas) en el código; probablemente es un proceso manual o de una herramienta externa (CRM). |

