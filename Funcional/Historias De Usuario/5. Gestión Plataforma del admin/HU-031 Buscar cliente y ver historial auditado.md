#### HU-031: Buscar cliente y ver historial auditado

| Campo | Detalle |
|:---:|:---:|
| **Actor** | Administrador del producto |
| **Historia** | Como administrador, quiero buscar un cliente por documento y ver su historial completo de operaciones auditadas, para resolver dudas o disputas rápidamente. |
| **Prioridad** | Media |
| **Criterios de aceptación** | El administrador busca por documento y consulta hasta 500 registros de auditoría del cliente (línea de crédito, desembolsos, pagos). |
| **Relaciones** | Casos de uso: CU-015. Requerimientos:[RF-030](../../Requerimientos/Requerimientos%20Funcionales.md),[RF-031](../../Requerimientos/Requerimientos%20Funcionales.md). |
| **Referencias** | `backends/admin/src/controllers/clients.controller.ts` (`getClientAuditedOperations`) — confirmado en `credits-platform-main`. |
 **Autor** | María Fernanda Herazo |
| **Fecha** | 18/08/2026 |
| **Versión** | V.1.7 |
| **Comentarios** | Implementada. El controlador `getClientAuditedOperations` en `backends/admin` sí existe y expone el historial auditado por cliente. |
