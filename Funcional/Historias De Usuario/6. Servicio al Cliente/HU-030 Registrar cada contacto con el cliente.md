
#### HU-030: Registrar cada contacto con el cliente

| Campo | Detalle |
|:---:|:---:|
| **Actor** | Agente de servicio al cliente |
| **Historia** | Como agente de servicio al cliente, quiero registrar cada contacto que se tiene con el cliente, sin importar el canal o el motivo, para mantener trazabilidad completa de toda la atención brindada, no solo de la gestión de cobranza. |
| **Prioridad** | Alta |
| **Criterios de aceptación** | Cada contacto con el cliente (por WhatsApp, correo, llamada, asistente virtual o agente humano) queda registrado con canal, motivo, resultado y fecha, disponible en el historial general de atención del cliente, independientemente de si el contacto está o no relacionado con cobranza. |
| **Relaciones** | Historias relacionadas: HU-006, HU-007, HU-016, HU-017, HU-025, HU-028, HU-029. |
| **Referencias** | Pendiente de verificar en código; ya existe un registro de notas de cobranza (`collection-notes.ts`, ver HU-025), pero no un registro general de contacto que cubra todos los flujos. |
 **Autor** | María Fernanda Herazo |
| **Fecha** | 18/08/2026 |
| **Versión** | V.1.7 |
| **Comentarios** | **Historia agregada en la v1.6**: aunque ya existe el registro de notas de gestión de cobranza (HU-025), también se debe guardar un registro de todo contacto con el cliente en general (KYC, biometría, atención por IA, atención humana, etc.), no solo el de cobranza. |