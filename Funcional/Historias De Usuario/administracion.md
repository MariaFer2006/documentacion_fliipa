# Administración

[← Volver al índice](README.md)

Cubre el portal administrativo: búsqueda de clientes con historial auditado, ajustes de cupo y fecha de corte, simulador de plan de pago, administración de la blacklist y monitoreo de salud del sistema.

**Historias en este capítulo:** HU-031 a HU-036.

---

## Administrador del producto (portal administrativo)

#### HU-031: Buscar cliente y ver historial auditado

| Campo | Detalle |
|:---:|:---:|
| **Actor** | Administrador del producto |
| **Historia** | Como administrador, quiero buscar un cliente por documento y ver su historial completo de operaciones auditadas, para resolver dudas o disputas rápidamente. |
| **Prioridad** | Media |
| **Criterios de aceptación** | El administrador busca por documento y consulta hasta 500 registros de auditoría del cliente (línea de crédito, desembolsos, pagos). |
| **Relaciones** | Casos de uso: CU-015. Requerimientos: RF-030, RF-031. |
| **Referencias** | `backends/admin/src/controllers/clients.controller.ts` (`getClientAuditedOperations`) — confirmado en `credits-platform-main`. |
| **Autor / Fecha / Versión** | María Fernanda Herazo |
| **Comentarios** | Implementada. El controlador `getClientAuditedOperations` en `backends/admin` sí existe y expone el historial auditado por cliente. |

#### HU-032: Ajustar cupo o fecha de corte

| Campo | Detalle |
|:---:|:---:|
| **Actor** | Administrador del producto |
| **Historia** | Como administrador, quiero ajustar el cupo o la fecha de corte de una línea de crédito, para corregir casos excepcionales autorizados por negocio. |
| **Prioridad** | Media |
| **Criterios de aceptación** | El administrador puede ajustar dentro de los rangos válidos, quedando la acción registrada en auditoría. |
| **Relaciones** | Casos de uso: CU-015. Requerimiento: RF-018. |
| **Referencias** | `backends/admin/src/controllers/credit-lines.controller.ts` — confirmado en `credits-platform-main`. |
| **Autor / Fecha / Versión** | María Fernanda Herazo |
| **Comentarios** | Implementada. Se confirma también el hallazgo de RF-018: el admin acepta `cutoffDay` en rango 0–31, mientras que redemption exige 1–31 — discrepancia real entre ambos módulos. |

#### HU-033: Simular plan de pago con distintas tasas

| Campo | Detalle |
|:---:|:---:|
| **Actor** | Administrador del producto |
| **Historia** | Como administrador, quiero simular el plan de pago de un cliente en mora con distintas tasas, para preparar acuerdos de pago o alivios. |
| **Prioridad** | Media |
| **Criterios de aceptación** | El administrador ingresa tasa corriente, tasa de mora y umbral de días, y obtiene el plan de pago diario descargable en CSV. |
| **Relaciones** | Casos de uso: CU-016. Requerimiento: RF-024. |
| **Referencias** | `backends/admin/src/controllers/calculator.controller.ts` (`getCalculatorStatus`, recibe `currentInterestRate`, `overdueInterestRate`, `thresholdDays`); descarga CSV en `apps/admin/src/lib/generate-csv-file.ts` y `apps/admin/src/app/disbursements/consult/CalculatorDownloaderButton.tsx` — confirmado en `credits-platform-main`. |
| **Autor / Fecha / Versión** | María Fernanda Herazo |
| **Comentarios** | Implementada, exactamente con los campos descritos en la historia (tasa corriente, tasa de mora, umbral de días) y con descarga CSV real. |

#### HU-034: Administrar la lista negra (blacklist)

| Campo | Detalle |
|:---:|:---:|
| **Actor** | Administrador del producto |
| **Historia** | Como administrador, quiero agregar o retirar clientes de la lista negra, para bloquear casos de fraude confirmado. |
| **Prioridad** | Alta |
| **Criterios de aceptación** | El administrador agrega o retira clientes de la blacklist, validando que el cliente exista y registrando el motivo por el cual el cliente ingresa a la lista negra. |
| **Relaciones** | Casos de uso: CU-017. Requerimiento: RF-027. Historia relacionada: HU-011 (capítulo [Onboarding](onboarding.md)), HU-035. |
| **Referencias** | `backends/b2b/src/controllers/blacklist/add-client-to-blacklist.ts`, `backends/b2b/src/controllers/blacklist/remove-client-client-from-blacklist.ts` |
| **Autor / Fecha / Versión** | María Fernanda Herazo |
| **Comentarios** | **Corrección v1.6**: se agrega al criterio de aceptación el registro del motivo de ingreso a la blacklist, que hacía falta. Pendiente de verificar en código si el modelo actual de blacklist tiene un campo de motivo o si debe agregarse. A diferencia de HU-031/032/033/036, esta historia sí tenía respaldo real desde la v1.3, pero en `backends/b2b` — no en un backend administrativo separado. Se confirma el hallazgo original: no hay enforcement de la blacklist sobre checkout, evaluación de riesgo o desembolso en ningún archivo del repositorio (`blacklists` solo aparece como relación de lectura en `get-client-by-id.service.ts`, sin ninguna validación bloqueante). Este es un riesgo de negocio real y verificado. |

#### HU-035: Consultar clientes en blacklist

| Campo | Detalle |
|:---:|:---:|
| **Actor** | Administrador del producto |
| **Historia** | Como administrador, quiero consultar la tabla de clientes en la lista negra (blacklist), para saber a quién no debo ofrecerle ningún producto o beneficio. |
| **Prioridad** | Alta |
| **Criterios de aceptación** | El administrador consulta, desde el panel administrativo, el listado completo de clientes en blacklist, incluyendo el motivo de ingreso registrado en HU-034. |
| **Relaciones** | Casos de uso: CU-017. Historia relacionada: HU-034. |
| **Referencias** | Pendiente de verificar en código si existe un endpoint o pantalla de listado de blacklist (más allá de agregar/retirar clientes de forma individual). |
| **Autor / Fecha / Versión** | María Fernanda Herazo |
| **Comentarios** | **Historia agregada en la v1.6**: no se encontró en el código revisado ninguna pantalla o endpoint dedicado a consultar el listado completo de blacklist; solo se identificaron los controladores para agregar y retirar clientes individualmente. |

#### HU-036: Monitorear salud del sistema en tiempo real

| Campo | Detalle |
|:---:|:---:|
| **Actor** | Administrador con rol de sistema (SYS_ADMIN) |
| **Historia** | Como administrador con rol de sistema, quiero ver el estado del core bancario y de la base de datos en tiempo real, para detectar incidentes antes de que afecten a los clientes. |
| **Prioridad** | Media |
| **Criterios de aceptación** | El administrador de sistema consulta latencia y disponibilidad del core bancario y de Cloud SQL desde el panel. |
| **Relaciones** | Casos de uso: CU-018. Requerimiento: RF-033. |
| **Referencias** | `backends/admin/src/controllers/system-core-health.controller.ts`, `system-cloud-sql.controller.ts` — confirmados en `credits-platform-main`. |
| **Autor / Fecha / Versión** | María Fernanda Herazo |
| **Comentarios** | Implementada, con un hallazgo adicional (ver RF-033): el monitoreo de terceros solo cubre GitHub, npm y GCP; no cubre Experian, Druo, el proveedor de biometría, Zenvia/Sendgrid ni el core bancario, a pesar de que la historia y el alcance del producto los describen como críticos para el negocio. |

---

[← Anterior: Servicio al cliente](servicio-cliente.md) · [Volver al índice](README.md)
