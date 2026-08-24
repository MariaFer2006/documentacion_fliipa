#### HU-010: Consultar cupo, plan de pagos y movimientos

| Campo | Detalle |
|:---:|:---:|
| **Actor** | Cliente empresarial |
| **Historia** | Como cliente empresarial, quiero consultar mi cupo disponible, mi plan de pagos y mis movimientos, para saber cuánto puedo usar y cuánto debo. |
| **Prioridad** | Alta |
| **Criterios de aceptación** | El cliente accede al portal de usuarios y visualiza cupo disponible, plan de pagos y movimientos, solo si su línea de crédito está en estado Aprobado o Activa. |
| **Relaciones** | Casos de uso: [CU-009](../../Casos%20de%20Uso/3.%20Credito/CU-009%20Consultar%20cupo%2C%20plan%20de%20pagos%20y%20disponibilidad%20de%20credito.md).Requerimientos:[RF-016](../../Requerimientos/Requerimientos%20Funcionales.md),[RF-017](../../Requerimientos/Requerimientos%20Funcionales.md). Historia relacionada: [HU-011](../3.%20Credito/HU-011%20Ver%20mensaje%20de%20no%20disponibilidad%20de%20cr%C3%A9dito.md). |
| **Referencias** | `b2b/fliipa-back/src/controllers/credit-line/get-credit-status.ts`, `credit-line/get-disbursements.ts`; `b2b/fliipa-redemption/actions/auth.ts` |
 **Autor** | María Fernanda Herazo |
| **Fecha** | 18/08/2026 |
| **Versión** | V.1.7 |
| **Comentarios** | Esta pantalla solo aplica para usuarios con creditos aprobados o activos. Los endpoints de estado de crédito y desembolsos existen y delegan en un cliente del core bancario (`coreApiClient`). La restricción exacta a estados `approved`/`active` no se verificó línea por línea; se recomienda confirmarla en la capa de autenticación de `fliipa-redemption/actions/auth.ts`. |

