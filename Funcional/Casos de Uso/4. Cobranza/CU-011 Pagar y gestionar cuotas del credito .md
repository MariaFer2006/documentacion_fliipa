### CU-011: Pagar y gestionar cuotas del crédito

![Diagrama de caso de uso CU-011](imagenes/diagrama_CU-011.svg)

| Campo | Detalle |
|---|---|
| **Actores** | Cliente empresarial; Sistema (Fliipa) |
| **Descripción** | El cliente puede prepagar su cuota antes de la fecha de corte mediante PSE, y el sistema gestiona el débito automático de créditos que superaron su fecha de pago y mantienen saldo pendiente. |
| **Precondiciones** | El cliente tiene una cuota vigente o vencida asociada a su línea de crédito. Para el débito automático, la cuenta bancaria del cliente debe estar conectada y vigente mediante Druo. |
| **Flujo principal** | 1. (Prepago) El cliente inicia el pago de su cuota en cualquier momento antes de la fecha de corte, mediante PSE.<br>2. El sistema refleja el pago en el plan de pagos y en el cupo disponible del cliente.<br>3. (Débito automático) El sistema identifica los créditos vencidos candidatos a débito automático según las reglas de cartera.<br>4. El sistema ejecuta el débito conforme a las reglas definidas y registra el resultado del intento. |
| **Flujos alternativos / excepciones** | A1. El pago por PSE no se completa: la cuota permanece pendiente.<br>A2. La cuenta Druo del cliente no está conectada o vigente: el crédito no es candidato a débito automático hasta reconectarla (ver CU-024). |
| **Postcondiciones** | La cuota queda pagada (por PSE o por débito automático) y reflejada en el plan de pagos y el cupo del cliente. |
| **Reglas de negocio** | El prepago por PSE y el débito automático son procesos distintos, aunque ambos usan Druo como conector bancario. |
| **Historias de usuario relacionadas** |[HU-013](../../Historias%20De%20Usuario/4.%20Cobranza/HU-013%20Prepagar%20la%20cuota%20por%20PSE.md) (Prepagar la cuota por PSE)<br>[HU-014](../../Historias%20De%20Usuario/4.%20Cobranza/HU-014%20Debito%20autom%C3%A1tico%20de%20cr%C3%A9ditos%20vencidos.md) (Débito automático de créditos vencidos)|
| **Estado en plataforma** | No se encontró implementación de pago por PSE en el repositorio (búsqueda de "PSE" sin coincidencias). Para el débito automático, solo está implementada la conexión de cuenta con Druo y la recepción de eventos asociados (`debit-bank-account.druo.ts`, `connect-bank-account.druo.ts`, `druo-events.webhook.ts`); el débito automático de punta a punta **no** está implementado como funcionalidad de producto. |
| **Referencias** | Fuente: fichas [HU-013](../../Historias%20De%20Usuario/4.%20Cobranza/HU-013%20Prepagar%20la%20cuota%20por%20PSE.md) y [HU-014](../../Historias%20De%20Usuario/4.%20Cobranza/HU-014%20Debito%20autom%C3%A1tico%20de%20cr%C3%A9ditos%20vencidos.md) — *Historias de Usuario — Fliipa*, carpeta "4. Cobranza" (repositorio `documentacion_fliipa`, María Fernanda Herazo). |
