# Servicio al cliente

[← Volver al índice](README.md)

Cubre la atención al cliente por asistente virtual con IA, el escalamiento a agente humano, la validación de identidad en casos críticos y el registro general de todo contacto con el cliente (más allá de la gestión de cobranza, documentada en el capítulo [Cobranza](cobranza.md)).

**Historias en este capítulo:** HU-016, HU-017, HU-028 a HU-030.

---

## Cliente empresarial

#### HU-016: Atención inicial por asistente virtual con IA

| Campo | Detalle |
|:---:|:---:|
| **Actor** | Cliente empresarial |
| **Historia** | Como cliente empresarial, quiero que un asistente virtual con inteligencia artificial atienda mi primer contacto por WhatsApp, para obtener respuesta inmediata a mis dudas más comunes. |
| **Prioridad** | Alta |
| **Criterios de aceptación** | El asistente virtual con IA recibe y responde el primer contacto del cliente por WhatsApp, dentro de las dudas frecuentes definidas en su alcance. |
| **Relaciones** | Casos de uso: CU-014. Requerimiento: RF-028. Historia relacionada: HU-017. |
| **Referencias** | [Reglas Negocio](../negocio/reglas-negocio/09-servicio-cliente.md); `b2b/services/communications/src/controllers/whatsapp/whatsapp.controller.ts` |
| **Autor / Fecha / Versión** | María Fernanda Herazo |
| **Comentarios** | **Historia separada de la HU-011 original (v1.5)**, que combinaba el flujo de atención por IA con el flujo de escalamiento a un agente humano; deben documentarse por separado para no interferir con los procesos ya definidos de servicio al cliente y de la operación. No se encontró en el código revisado ningún módulo de asistente conversacional de IA ni lógica de escalamiento; los controladores del microservicio `communications` están limitados a envío de OTP, firma y contrato por WhatsApp/correo. Probablemente vive en una herramienta externa no incluida en este repositorio. |

#### HU-017: Escalar a agente humano cuando la IA no resuelve el caso

| Campo | Detalle |
|:---:|:---:|
| **Actor** | Cliente empresarial |
| **Historia** | Como cliente empresarial, quiero que mi caso se escale a un agente humano cuando el asistente virtual no logre resolverlo, para no depender únicamente de canales automatizados. |
| **Prioridad** | Alta |
| **Criterios de aceptación** | Cuando el asistente virtual no resuelve el caso del cliente, el sistema escala el caso a un agente humano junto con el contexto completo de la conversación. |
| **Relaciones** | Casos de uso: CU-014. Requerimiento: RF-029. Historias relacionadas: HU-016, HU-028. |
| **Referencias** | [Reglas Negocio](../negocio/reglas-negocio/09-servicio-cliente.md) |
| **Autor / Fecha / Versión** | María Fernanda Herazo |
| **Comentarios** | **Historia separada de la HU-011 original (v1.5)**. No se encontró lógica de escalamiento en el código revisado; corresponde al mismo hallazgo documentado en HU-016 y en HU-028 (antes HU-022). |

## Agente de servicio al cliente

#### HU-028: Recibir el caso escalado con contexto completo

| Campo | Detalle |
|:---:|:---:|
| **Actor** | Agente de servicio al cliente |
| **Historia** | Como agente de servicio al cliente, quiero recibir el caso escalado por la IA con el contexto completo de la conversación, para no pedirle al cliente que repita su problema. |
| **Prioridad** | Alta |
| **Criterios de aceptación** | Cuando la IA escala un caso, el agente humano ve el historial completo de la conversación antes de responder. |
| **Relaciones** | Casos de uso: CU-014. Requerimiento: RF-028. Historia relacionada: HU-017. |
| **Referencias** | [Reglas Negocio](../negocio/reglas-negocio/09-servicio-cliente.md) |
| **Autor / Fecha / Versión** | María Fernanda Herazo |
| **Comentarios** | Se confirma la separación entre el flujo de atención por IA (HU-016) y el de escalamiento/gestión humana (esta historia y HU-017): son procesos distintos y deben documentarse por separado. Confirmado (ver HU-016/HU-017): no existe módulo de IA conversacional ni de escalamiento en el código de `communications` ni en ningún otro servicio revisado. |

#### HU-029: Validar identidad en casos críticos

| Campo | Detalle |
|:---:|:---:|
| **Actor** | Agente de servicio al cliente |
| **Historia** | Como agente de servicio al cliente, quiero validar la identidad del cliente antes de aprobar un caso crítico (suplantación, uso indebido del cupo), para evitar fraude. |
| **Prioridad** | Alta |
| **Criterios de aceptación** | Los casos críticos requieren validación de identidad y aprobación manual explícita del agente antes de cerrarse. |
| **Relaciones** | Casos de uso: CU-014. Requerimiento: RF-029. |
| **Referencias** | [Reglas Negocio](../negocio/reglas-negocio/09-servicio-cliente.md) |
| **Autor / Fecha / Versión** | María Fernanda Herazo |
| **Comentarios** | Sin código de respaldo encontrado; es consistente con la ausencia general de un módulo de servicio al cliente/IA en el repositorio. |

#### HU-030: Registrar cada contacto con el cliente

| Campo | Detalle |
|:---:|:---:|
| **Actor** | Agente de servicio al cliente |
| **Historia** | Como agente de servicio al cliente, quiero registrar cada contacto que se tiene con el cliente, sin importar el canal o el motivo, para mantener trazabilidad completa de toda la atención brindada, no solo de la gestión de cobranza. |
| **Prioridad** | Alta |
| **Criterios de aceptación** | Cada contacto con el cliente (por WhatsApp, correo, llamada, asistente virtual o agente humano) queda registrado con canal, motivo, resultado y fecha, disponible en el historial general de atención del cliente, independientemente de si el contacto está o no relacionado con cobranza. |
| **Relaciones** | Historias relacionadas: HU-006, HU-007 (capítulo [Onboarding](onboarding.md)), HU-016, HU-017, HU-025 (capítulo [Cobranza](cobranza.md)), HU-028, HU-029. |
| **Referencias** | Pendiente de verificar en código; ya existe un registro de notas de cobranza (`collection-notes.ts`, ver HU-025), pero no un registro general de contacto que cubra todos los flujos. |
| **Autor / Fecha / Versión** | María Fernanda Herazo |
| **Comentarios** | **Historia agregada en la v1.6**: aunque ya existe el registro de notas de gestión de cobranza (HU-025), también se debe guardar un registro de todo contacto con el cliente en general (KYC, biometría, atención por IA, atención humana, etc.), no solo el de cobranza. |

---

[← Anterior: Cobranza](cobranza.md) · [Volver al índice](README.md) · [Siguiente: Administración →](administracion.md)
