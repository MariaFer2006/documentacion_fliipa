### HU-014: Débito automático de créditos vencidos

| Campo | Detalle |
|:---:|:---:|
| **Actor** | Sistema (Fliipa) |
| **Historia** | Como Fliipa, quiero gestionar el débito automático de créditos que hayan superado su fecha de pago y mantengan un saldo pendiente, para facilitar el recaudo de la cartera vencida sin depender de una acción manual del cliente. |
| **Prioridad** | Alta |
| **Criterios de aceptación** | El sistema debe identificar los créditos vencidos que podrían ser candidatos a débito automático de acuerdo con las reglas de cartera definidas. La cuenta bancaria del cliente debe estar previamente conectada y vigente mediante Druo. Cuando el débito automático de cartera vencida esté habilitado como producto, el sistema deberá ejecutar el débito conforme a las reglas definidas y registrar el resultado del intento. |
| **Relaciones** | Casos de uso: CU-011. Requerimiento: RF-022. Historia relacionada: HU-013. |
| **Referencias** | `b2b/fliipa-back/src/services/druo/debit-bank-account.druo.ts`, `connect-bank-account.druo.ts`; `b2b/fliipa-back/src/controllers/webhooks/druo-events.webhook.ts` |
| **Autor / Fecha / Versión** | María Fernanda Herazo |
| **Comentarios** | **Corrección v1.6:** actualmente está implementada la conexión de la cuenta bancaria mediante Druo y existen mecanismos para recibir avisos/eventos relacionados con dicha conexión. Sin embargo, el **débito automático de una cuota vencida de punta a punta todavía no está implementado como funcionalidad de producto**. Por tanto, esta historia no debe marcarse como implementada. La existencia de `debit-bank-account.druo.ts` no es suficiente para afirmar que el flujo completo de cobro automático de cartera vencida está operativo. |
