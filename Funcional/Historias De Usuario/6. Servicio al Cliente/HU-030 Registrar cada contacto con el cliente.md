
#### HU-030: Registrar cada contacto con el cliente

| Campo | Detalle |
|:---:|:---:|
| **Actor** | Agente de servicio al cliente |
| **Historia** | Como agente de servicio al cliente, quiero registrar cada contacto que se tiene con el cliente, sin importar el canal o el motivo, para mantener trazabilidad completa de toda la atención brindada, no solo de la gestión de cobranza. |
| **Prioridad** | Alta |
| **Criterios de aceptación** | Cada contacto con el cliente (por WhatsApp, correo, llamada, asistente virtual o agente humano) queda registrado con canal, motivo, resultado y fecha, disponible en el historial general de atención del cliente, independientemente de si el contacto está o no relacionado con cobranza. |
| **Relaciones** | Historias relacionadas:[HU-006](../2.%20KYC/HU-006%20Completar%20la%20validaci%C3%B3n%20biom%C3%A9trica%20(KYC).md),[HU-007](../2.%20KYC/HU-007%20Cargar%20soportes%20bancarios.md), [HU-016](../6.%20Servicio%20al%20Cliente/HU-016%20Atencion%20inicial%20por%20asistente%20virtual%20con%20IA.md), [HU-017](../6.%20Servicio%20al%20Cliente/HU-017%20Escalar%20a%20agente%20humano%20cuando%20la%20IA%20no%20resuelve%20el%20caso.md), [HU-025](../4.%20Cobranza/HU-025%20Registrar%20cada%20interacci%C3%B3n%20de%20cobranza.md), [HU-028](../6.%20Servicio%20al%20Cliente/HU-028%20Recibir%20el%20caso%20escalado%20con%20contexto%20completo.md), [HU-029](../6.%20Servicio%20al%20Cliente/HU-029%20Validar%20identidad%20en%20casos%20cr%C3%ADticos.md). |
| **Referencias** | Pendiente de verificar en código; ya existe un registro de notas de cobranza (`collection-notes.ts`, ver HU-025), pero no un registro general de contacto que cubra todos los flujos. |
 **Autor** | María Fernanda Herazo |
| **Fecha** | 18/08/2026 |
| **Versión** | V.1.7 |
| **Comentarios** | **Historia agregada en la v1.6**: aunque ya existe el registro de notas de gestión de cobranza (HU-025), también se debe guardar un registro de todo contacto con el cliente en general (KYC, biometría, atención por IA, atención humana, etc.), no solo el de cobranza. |










