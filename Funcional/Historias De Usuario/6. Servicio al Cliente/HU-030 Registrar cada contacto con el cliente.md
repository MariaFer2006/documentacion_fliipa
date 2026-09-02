
#### HU-030: Registrar cada contacto con el cliente

| Campo | Detalle |
|:---:|:---:|
| **Actor** | Agente de servicio al cliente |
| **Historia** | Como agente de servicio al cliente, quiero registrar cada contacto que se tiene con el cliente, sin importar el canal o el motivo, para mantener trazabilidad completa de toda la atenci贸n brindada, no solo de la gesti贸n de cobranza. |
| **Prioridad** | Alta |
| **Criterios de aceptaci贸n** | Cada contacto con el cliente (por WhatsApp, correo, llamada, asistente virtual o agente humano) queda registrado con canal, motivo, resultado y fecha, disponible en el historial general de atenci贸n del cliente, independientemente de si el contacto est谩 o no relacionado con cobranza. |
| **Relaciones** | Historias relacionadas:[HU-006](../1. Onboarding/HU-006%20Completar%20la%20validaci%C3%B3n%20biom%C3%A9trica%20%28KYC%29.md),[HU-007](../2. KYC/HU-007 Cargar soportes bancarios.md), [HU-016](../6. Servicio al Cliente/HU-016 Atencion inicial por asistente virtual con IA.md), [HU-017](../6. Servicio al Cliente/HU-017 Escalar a agente humano cuando la IA no resuelve el caso.md), [HU-025](../4. Cobranza/HU-025 Registrar cada interacci髇 de cobranza.md), [HU-028](../6. Servicio al Cliente/HU-028 Recibir el caso escalado con contexto completo.md), [HU-029](../6. Servicio al Cliente/HU-029 Validar identidad en casos cr韙icos.md). |
| **Referencias** | Pendiente de verificar en c贸digo; ya existe un registro de notas de cobranza (`collection-notes.ts`, ver HU-025), pero no un registro general de contacto que cubra todos los flujos. |
 **Autor** | Mar铆a Fernanda Herazo |
| **Fecha** | 18/08/2026 |
| **Versi贸n** | V.1.7 |
| **Comentarios** | **Historia agregada en la v1.6**: aunque ya existe el registro de notas de gesti贸n de cobranza (HU-025), tambi茅n se debe guardar un registro de todo contacto con el cliente en general (KYC, biometr铆a, atenci贸n por IA, atenci贸n humana, etc.), no solo el de cobranza. |










