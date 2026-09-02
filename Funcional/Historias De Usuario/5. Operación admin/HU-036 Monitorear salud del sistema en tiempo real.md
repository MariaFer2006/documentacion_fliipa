#### HU-036: Monitorear salud del sistema en tiempo real

| Campo | Detalle |
|:---:|:---:|
| **Actor** | Administrador con rol de sistema (SYS_ADMIN) |
| **Historia** | Como administrador con rol de sistema, quiero ver el estado del core bancario y de la base de datos en tiempo real, para detectar incidentes antes de que afecten a los clientes. |
| **Prioridad** | Baja|
| **Criterios de aceptación** | El administrador de sistema consulta latencia y disponibilidad del core bancario y de Cloud SQL desde el panel. |
| **Relaciones** | Casos de uso: [CU-018](../../Casos de Uso/6. Operaci�n Admin/CU-018 Monitorear salud del sistema en tiempo real.md). Requerimiento: [RF-033](../../Requerimientos/Requerimientos Funcionales.md). |
| **Referencias** | `backends/admin/src/controllers/system-core-health.controller.ts`, `system-cloud-sql.controller.ts` — confirmados en `credits-platform-main`. |
 **Autor** | María Fernanda Herazo |
| **Fecha** | 18/08/2026 |
| **Versión** | V.1.7 |
| **Comentarios** | Implementada, con un hallazgo adicional (ver RF-033): el monitoreo de terceros solo cubre GitHub, npm y GCP; no cubre Experian, Druo, el proveedor de biometría, Zenvia/Sendgrid ni el core bancario, a pesar de que la historia y el alcance del producto los describen como críticos para el negocio. |
