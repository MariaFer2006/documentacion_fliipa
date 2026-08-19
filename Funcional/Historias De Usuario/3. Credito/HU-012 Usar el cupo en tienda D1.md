#### HU-012: Usar el cupo en tienda D1

| Campo | Detalle |
|:---:|:---:|
| **Actor** | Cliente empresarial |
| **Historia** | Como cliente empresarial, quiero visualizar un código de compra para usar mi cupo en la tienda D1, para pagar mi mercancía sin dinero en efectivo. |
| **Prioridad** | Alta |
| **Criterios de aceptación** | El cliente obtiene un código de compra y el punto de venta D1 lo valida para aplicar el cupo a la compra. |
| **Relaciones** | Casos de uso: [CU-010](../../Casos%20de%20Uso/3.%20Credito/CU-010%20Usar%20el%20cupo%20en%20tienda%20D1.md). Requerimientos: [RF-019](../../Requerimientos/Requerimientos%20Funcionales.md),[RF-020](../../Requerimientos/Requerimientos%20Funcionales.md),. |
| **Referencias** | `b2b/fliipa-back/src/controllers/qr/get-or-create-qr.ts`, `qr/validate-qr.ts`, `clients/get-client-coupon.ts` |
 **Autor** | María Fernanda Herazo |
| **Fecha** | 18/08/2026 |
| **Versión** | V.1.7 |
| **Comentarios** | **Corrección v1.5:** la historia se limita al código de compra/cupón, que sí cuenta con referencia funcional en el repositorio. |
