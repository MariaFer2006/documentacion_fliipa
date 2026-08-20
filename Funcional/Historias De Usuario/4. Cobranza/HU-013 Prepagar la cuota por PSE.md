#### HU-013: Prepagar la cuota por PSE

| Campo | Detalle |
|:---:|:---:|
| **Actor** | Cliente empresarial |
| **Historia** | Como cliente empresarial, quiero prepagar mi cuota antes de su fecha de vencimiento mediante PSE, para no incurrir en mora y mantener un buen comportamiento de crédito. |
| **Prioridad** | Media |
| **Criterios de aceptación** | El cliente puede realizar el pago de su cuota en cualquier momento antes de la fecha de vencimiento (30 días después del desembolso) mediante PSE, y el sistema refleja el pago en su plan de pagos y en su cupo disponible. |
| **Relaciones** | Casos de uso: [CU-011](../../Casos%20de%20Uso/4.%20Cobranza/CU-011%20Pagar%20y%20gestionar%20cuotas%20del%20credito%20.md) Requerimiento:  [RF-022](../../Requerimientos/Requerimientos%20Funcionales.md). Historia relacionada: [HU-014](../4.%20Cobranza/HU-014%20Debito%20autom%C3%A1tico%20de%20cr%C3%A9ditos%20vencidos.md). |
| **Referencias** | [Procesos](../../../Operaciones/Procesos/07%20Modelo%20Cobranza.md); no se encontró implementación de pago por PSE en ningún archivo del repositorio (se buscó "PSE" en todo el proyecto sin coincidencias). |
| **Autor** | María Fernanda Herazo |
| **Fecha** | 20/08/2026 |
| **Versión** | V.1.8 |
| **Comentarios** | **Historia separada de la HU-009 original (v1.5)**, que combinaba prepago y débito automático en un solo paso; aunque ambos son pagos y ambos usan Druo, son procesos distintos que pertenecen a flujos diferentes. **Corrección v1.8 (Check-in de Producto, 20 ago 2026):** se elimina la referencia a "fecha de corte", concepto que el producto actual no maneja; el crédito vence 30 días después del desembolso, por lo que se reemplaza por "fecha de vencimiento". Se mantiene pendiente de confirmar con el equipo técnico si el prepago por PSE vive en un microservicio no incluido en este repositorio. |




