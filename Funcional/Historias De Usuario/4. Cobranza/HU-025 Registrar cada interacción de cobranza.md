#### HU-025: Registrar cada interacción de cobranza

| Campo | Detalle |
|:---:|:---:|
| **Actor** | Analista de cartera |
| **Historia** | Como analista de cartera, quiero registrar cada interacción de cobranza (canal, tipo de contacto, resultado, compromiso de pago), para mantener trazabilidad completa del caso. |
| **Prioridad** | Alta |
| **Criterios de aceptación** | El analista registra canal, tipo de contacto, resultado y monto comprometido de cada interacción, quedando disponible en el resumen de atención del cliente. |
| **Relaciones** | Casos de uso: [CU-012](../../Casos%20de%20Uso/4.%20Cobranza/CU-012%20Gestionar%20y%20registrar%20cartera%20y%20cobranza.md). Requerimientos: [RF-025](../../Requerimientos/Requerimientos%20Funcionales.md),[RF-026](../../Requerimientos/Requerimientos%20Funcionales.md). Historia relacionada: [HU-030](../6.%20Servicio%20al%20Cliente/HU-030%20Registrar%20cada%20contacto%20con%20el%20cliente.md)  |
| **Referencias** | `b2b/fliipa-back/src/controllers/clients/collection-notes.ts` |
 **Autor** | María Fernanda Herazo |
| **Fecha** | 18/08/2026 |
| **Versión** | V.1.7 |
| **Comentarios** | **Confirmado**: el módulo está completamente implementado — creación, edición, eliminación y listado de notas de cobranza, más un resumen de atención (`getCollectionNotesAttentionSummary`). Ver HU-030 (nueva en v1.6) para el registro de contacto general, más allá de cobranza. |

