### CU-014: Atender al cliente por IA y escalar a agente humano

![Diagrama de caso de uso CU-014](imagenes/diagrama_CU-014.svg)

| Campo | Detalle |
|:---:|:---:|
| **Actores** | Cliente empresarial; Asistente virtual (IA); Agente de servicio al cliente |
| **Descripción** | Un asistente virtual con IA atiende el primer contacto del cliente por WhatsApp; si no logra resolver el caso, lo escala a un agente humano junto con el contexto completo de la conversación, y en casos críticos (suplantación, uso indebido del cupo) el agente valida la identidad del cliente antes de aprobar el caso. |
| **Precondiciones** | El cliente inicia contacto por WhatsApp con una duda, solicitud o inquietud. |
| **Flujo principal** | 1. El cliente escribe por WhatsApp. 2. El asistente virtual con IA recibe y responde dentro de las dudas frecuentes definidas en su alcance. 3. Si el asistente no logra resolver el caso, el sistema lo escala a un agente humano. 4. El agente humano recibe el caso con el historial completo de la conversación, sin necesidad de que el cliente repita su problema. 5. Si el caso es crítico (suplantación, uso indebido del cupo), el agente valida la identidad del cliente antes de aprobar el caso, con aprobación manual explícita. |
| **Flujos alternativos / excepciones** | A1. El asistente resuelve el caso sin necesidad de escalamiento: el flujo termina en el paso 2. A2. El caso crítico no pasa la validación de identidad: no se aprueba y queda pendiente de revisión adicional. |
| **Postcondiciones** | El cliente recibe una respuesta a su consulta, ya sea por IA o por un agente humano, y los casos críticos quedan validados antes de cerrarse. |
| **Reglas de negocio** | Los casos críticos requieren validación de identidad y aprobación manual explícita antes de cerrarse. La atención por IA y el escalamiento a humano son procesos distintos que deben documentarse y operar por separado. |
| **Historias de usuario relacionadas** | HU-016 (Atención inicial por asistente virtual con IA), HU-017 (Escalar a agente humano cuando la IA no resuelve el caso), HU-028 (Recibir el caso escalado con contexto completo), HU-029 (Validar identidad en casos críticos) |
| **Estado en plataforma** | No se encontró en el código revisado ningún módulo de asistente conversacional de IA ni lógica de escalamiento; los controladores del microservicio `communications` se limitan al envío de OTP, firma y contrato por WhatsApp/correo. Probablemente vive en una herramienta externa no incluida en este repositorio. |
| **Referencias** | Fuente: fichas HU-016, HU-017, HU-028 y HU-029 — *Historias de Usuario — Fliipa*, carpeta "5. Servicio al Cliente" (repositorio `documentacion_fliipa`, María Fernanda Herazo). |
