#### HU-032: Ver historial auditado del cliente

| Campo | Detalle |
|:---:|:---:|
| **Actor** | Administrador del producto |
| **Historia** | Como administrador, quiero ver el historial completo de operaciones auditadas de un cliente (línea de crédito, desembolsos, pagos), para resolver dudas o disputas rápidamente sin depender de otro equipo. |
| **Prioridad** | Media |
| **Criterios de aceptación** | Una vez ubicado el cliente (ver HU-031), el administrador consulta hasta 500 registros de auditoría asociados a ese cliente, incluyendo cambios sobre su línea de crédito, sus desembolsos y sus pagos. |
| **Relaciones** | Casos de uso: [CU-015](../../Casos de Uso/6. Operaci�n Admin/CU-015 Buscar cliente, ver historial auditado y ajustar cupo o fecha de corte.md). Requerimiento: [RF-031](../../Requerimientos/Requerimientos Funcionales.md). Historia relacionada: [HU-031](../5. Operaci�n admin/HU-031 Buscar cliente por documento.md). |
| **Referencias** | `backends/admin/src/controllers/clients.controller.ts` (`listClientAuditedOperations` → `getClientAuditedOperations`); `backends/admin/src/routes.ts` (`GET /clients/:id/audited-operations`) — confirmado en `credits-platform-main`. |
| **Autor** | María Fernanda Herazo |
| **Fecha** | 20/08/2026 |
| **Versión** | V.1.0 |
| **Comentarios** | **Historia nueva, desprendida de HU-031 v1.7** (Check-in de Producto, 20 ago 2026). El controlador `getClientAuditedOperations`, expuesto en el endpoint `GET /clients/:id/audited-operations`, sí existe y respalda esta historia como **implementada**. |