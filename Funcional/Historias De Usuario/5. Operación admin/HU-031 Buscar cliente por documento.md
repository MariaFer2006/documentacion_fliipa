#### HU-031: Buscar cliente por documento de identificación

| Campo | Detalle |
|:---:|:---:|
| **Actor** | Administrador del producto |
| **Historia** | Como administrador, quiero buscar un cliente por documento de Identificación, para ubicar rápidamente su ficha y resolver dudas o disputas. |
| **Prioridad** | Media |
| **Criterios de aceptación** | El administrador busca clientes por documento (o por término libre) desde el panel, con resultados paginados. El sistema retorna el listado de clientes que coinciden con el criterio de búsqueda. El administrador puede además consultar el detalle de un cliente puntual por su identificador. |
| **Relaciones** | Casos de uso: [CU-015](../../Casos de Uso/6. Operaci�n Admin/CU-015 Buscar cliente, ver historial auditado y ajustar cupo o fecha de corte.md). Requerimiento: [RF-030](../../Requerimientos/Requerimientos Funcionales.md). Historia relacionada: [HU-032](../5. Operaci�n admin/HU-032 Ver historial auditado del cliente.md). |
| **Referencias** | `backends/admin/src/controllers/clients.controller.ts` (`listClients`, `getClient`); `backends/admin/src/routes.ts` (`GET /clients`, `GET /clients/:id`) — confirmado en `credits-platform-main`. |
| **Autor** | María Fernanda Herazo |
| **Fecha** | 20/08/2026 |
| **Versión** | V.1.8 |
| **Comentarios** | **Historia dividida (Check-in de Producto, 20 ago 2026):** se separa de la HU-031 original (v1.7), que combinaba búsqueda de cliente y visualización de historial auditado en un solo criterio de aceptación. Al ser dos endpoints y dos necesidades distintas (`listClients`/`getClient` vs. `listClientAuditedOperations`), se documentan como historias atómicas. El historial auditado queda en [HU-032](../5. Operaci�n admin/HU-032 Ver historial auditado del cliente.md). |