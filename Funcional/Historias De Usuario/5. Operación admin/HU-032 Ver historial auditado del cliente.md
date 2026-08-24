#### HU-032: Ver historial auditado del cliente

| Campo | Detalle |
|:---:|:---:|
| **Actor** | Administrador del producto |
| **Historia** | Como administrador, quiero ver el historial completo de operaciones auditadas de un cliente (línea de crédito, desembolsos, pagos), para resolver dudas o disputas rápidamente sin depender de otro equipo. |
| **Prioridad** | Media |
| **Criterios de aceptación** | Una vez ubicado el cliente (ver HU-031), el administrador consulta hasta 500 registros de auditoría asociados a ese cliente, incluyendo cambios sobre su línea de crédito, sus desembolsos y sus pagos. |
| **Relaciones** | Casos de uso: [CU-015](../../Casos%20de%20Uso/6.%20Operaci%C3%B3n%20Admin/CU-015%20Buscar%20cliente%2C%20ver%20historial%20auditado%20y%20ajustar%20cupo%20o%20fecha%20de%20corte.md). Requerimiento: [RF-031](../../Requerimientos/Requerimientos%20Funcionales.md). Historia relacionada: [HU-031](../5.%20Operaci%C3%B3n%20admin/HU-031%20Buscar%20cliente%20por%20documento.md). |
| **Referencias** | `backends/admin/src/controllers/clients.controller.ts` (`listClientAuditedOperations` → `getClientAuditedOperations`); `backends/admin/src/routes.ts` (`GET /clients/:id/audited-operations`) — confirmado en `credits-platform-main`. |
| **Autor** | María Fernanda Herazo |
| **Fecha** | 20/08/2026 |
| **Versión** | V.1.0 |
| **Comentarios** | **Historia nueva, desprendida de HU-031 v1.7** (Check-in de Producto, 20 ago 2026). El controlador `getClientAuditedOperations`, expuesto en el endpoint `GET /clients/:id/audited-operations`, sí existe y respalda esta historia como **implementada**. |