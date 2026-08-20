# Requerimientos Funcionales

| Documento | Requerimientos Funcionales |
|-----------|------------------------------|
| **Proyecto** | Fliipa |
| **Versión** | 1.1 |
| **Estado** | En revisión |
| **Responsable** | Producto, negocio y QA |
| **Última actualización** | 2026-07-10 |

---

## Control de versiones

| Versión | Fecha | Autor | Descripción |
|---------|-------|-------|-------------|
| 0.1 | 2026-07-06 | Maria Fernanda Herazo | Borrador vacío (pendiente de completar). |
| 1.0 | 2026-07-10 | María Fernanda Herazo | Primera versión completa: 35 requerimientos funcionales organizados en tablas por módulo, con estado de implementación verificado contra el código fuente de `credits-platform-main`. |
| 1.1 | 2026-07-10 | María Fernanda Herazo  | Se amplía cada requerimiento con nombre corto, descripción detallada, actor(es) involucrados y prioridad, según los criterios de priorización de [Alcance del Producto](../../producto/alcance.md#criterios-de-priorización). |
| 1.2 | 2026-07-30 | Maria Fernanda Herazo Escobar  | Se corrigen 5 requerimientos (RF-005, RF-008, RF-010, RF-011, RF-015) marcados como "no verificable" en la v1.1: esa revisión no había cubierto la carpeta `services/` del repositorio (motor de reglas, evaluaciones de riesgo, aprobación de líneas de crédito), donde sí existe evidencia real. Ver detalle en cada fila corregida. |
| 1.3 | 2026-08-13 | María Fernanda Herazo | Se corrige RF-006 para que ya no incluya la firma de contrato dentro de la validación por OTP (queda limitada a teléfono y correo del onboarding). Se reescribe RF-013 ("OTP de firma" → "Firma digital con proveedor externo"): la firma del contrato ya no ocurre mediante código OTP, según retroalimentación de negocio ya reflejada en HU-009 de Historias de Usuario. |
| 1.4 | 2026-08-20 | María Fernanda Herazo | Se agrega RF-036 (Visualización y confirmación del cupo aprobado), separado de RF-010 (consulta de riesgo crediticio del analista). Corresponde a la nueva historia HU-045 en Historias de Usuario, desprendida de HU-023. |

---

## Objetivo

Enumerar las capacidades que el sistema Fliipa debe cubrir, agrupadas por módulo, con su estado de implementación verificado contra el código fuente de `credits-platform-main` a la fecha de esta revisión.

## Alcance

Cubre los 11 procesos de negocio definidos en [Alcance del Producto](../../producto/alcance.md). Cada requerimiento usa el identificador `RF-XXX` de [Convenciones](../../CONVENCIONES.md). La columna "Prioridad" sigue los criterios de priorización del alcance del producto (Alta: valida el modelo de negocio, reduce fraude, disminuye riesgo, mejora experiencia del cliente, aumenta uso del crédito o garantiza sostenibilidad financiera; Media: automatiza procesos internos; Baja: mejora continua). La columna "Estado" indica si el requerimiento está implementado, parcialmente implementado o pendiente, según lo verificado en el repositorio de código; cuando no fue posible confirmarlo (por ejemplo, lógica que vive en microservicios no incluidos en el repositorio revisado) se indica explícitamente. No incluye requisitos de calidad, seguridad o desempeño (ver [Requerimientos No Funcionales](02-requerimientos-no-funcionales.md)).

## Documentos relacionados

- [Funcional](../README.md)
- [Flipa - Biblioteca de Conocimiento](../../README.md)
- [Mapa Del Conocimiento](../../MAPA_DEL_CONOCIMIENTO.md)
- [Onboarding](../../ONBOARDING.md)
- [Convenciones](../../CONVENCIONES.md)
- [Negocio](../../negocio/README.md)
- [Tecnico](../../tecnico/README.md)
- [Qa](../../qa/README.md)
- [Documento Funcional](../01-marco-funcional/01-documento-funcional.md)
- [Casos De Uso](../02-casos-de-uso/01-casos-de-uso.md)
- [Historias Usuario](../03-historias-usuario/01-historias-usuario.md)
- [Requerimientos No Funcionales](02-requerimientos-no-funcionales.md)

## Contenido

### Captación comercial

| ID | Nombre | Descripción | Actor(es) | Prioridad | Estado | Fuente |
|----|--------|--------------|-----------|-----------|--------|--------|
| RF-001 | Contacto simultáneo multicanal | El sistema debe permitir contactar simultáneamente al cliente preaprobado por correo, WhatsApp y llamada, a partir de la base de clientes preaprobados de D1. | Asesor comercial, cliente empresarial | Alta | Sin evidencia de automatización propia en el código; gestionado probablemente desde herramientas comerciales externas. | `backends/b2b` (sin controlador encontrado) |

### Onboarding digital

| ID | Nombre | Descripción | Actor(es) | Prioridad | Estado | Fuente |
|----|--------|--------------|-----------|-----------|--------|--------|
| RF-002 | Creación de solicitud (checkout) | Crear una solicitud a partir de documento y tipo de documento, reutilizando la solicitud existente en estado `REQUEST_STARTED` si el cliente aún no la ha completado. | Cliente empresarial | Alta | Implementado | `backends/b2b/src/controllers/checkouts/create-checkout.ts` |
| RF-003 | Prevención de solicitudes duplicadas | Impedir que un mismo documento inicie más de una solicitud si ya existe un cliente registrado con ese documento. | Sistema (automático) | Alta | Implementado | `checkouts/create-checkout.ts` |
| RF-004 | Actualización incremental del checkout | Permitir actualizar los datos del checkout (negocio, ubicación, representante legal, cuenta bancaria) de forma incremental, en varios pasos. | Cliente empresarial | Alta | Implementado | `checkouts/update-checkout.ts` |
| RF-005 | Cálculo del cupo preaprobado | Calcular y mostrar al cliente el cupo preaprobado con base en criterios de consumo histórico en D1. | Sistema (automático) | Alta | Implementado: el motor de reglas calcula un cupo sugerido a partir de `total_compras`, `num_compras` y `num_tiendas` del histórico D1, con multiplicadores según el volumen de compras. | `services/product/rules-engine/src/utils/get-suggested-credit.ts`, `services/product/rules-engine/src/rule-models/b2b-base-preapproval.ts` |

### Validación de identidad

| ID | Nombre | Descripción | Actor(es) | Prioridad | Estado | Fuente |
|----|--------|--------------|-----------|-----------|--------|--------|
| RF-006 | Validación por código de verificación | Enviar y validar códigos de verificación por teléfono y correo durante el onboarding, con reintentos y tiempo de bloqueo configurables. No cubre la firma de contrato, que se realiza mediante un proveedor externo de firma digital (ver RF-013). | Cliente empresarial, sistema | Alta | Implementado (ver hallazgo de seguridad en [RNF-001](02-requerimientos-no-funcionales.md#seguridad)) | `backends/b2b/src/controllers/otp/*.ts`, `backends/b2b/src/config/constants.ts` |
| RF-007 | Carga de documentos de soporte | Permitir cargar documento de identidad y certificación bancaria, restringiendo los tipos de archivo aceptados. | Cliente empresarial | Alta | Implementado | `clients/upload-document.ts` |
| RF-008 | Validación biométrica (KYC) | Ejecutar la validación biométrica del cliente y derivar a revisión manual los casos ambiguos ("en revisión"). | Cliente empresarial, analista de riesgo | Alta | Parcialmente implementado, con hallazgo: existe captura de selfie y foto de cédula (frente/reverso) en el checkout, revisable manualmente desde el panel admin. No se encontró ningún proveedor de biometría automatizado (ni Olimpia, citado en negocio/técnico, ni ningún otro) que ejecute la validación o derive casos ambiguos automáticamente; hoy toda la revisión es manual. | `apps/checkout/app/checkout/[id]/steps/SelfieStep.tsx`, `IdPhotoStep.tsx`, `apps/admin/src/app/product/clients/[id]/components/client-photos-tab.tsx` |
| RF-009 | Registro y validación del Cliente | Permitir registrar y validar al Cliente asociado al checkout (documento, teléfono, correo). | Cliente empresarial | Alta | Implementado | `clients/add-legal-representative.ts`, `clients/validate-legal-representative.ts` |

### Evaluación de riesgo

| ID | Nombre | Descripción | Actor(es) | Prioridad | Estado | Fuente |
|----|--------|--------------|-----------|-----------|--------|--------|
| RF-010 | Consulta de riesgo crediticio | Consultar Experian y el histórico transaccional de D1 para evaluar el riesgo del cliente. | Sistema (automático) | Alta | Implementado, con hallazgo: sí existe lógica real de invocación (validación de empresa/persona vía Experian, score vía Datacrédito). Hallazgo: 4 de 6 archivos de la integración Experian son mocks explícitos (`USE_MOCK = true` o comentario `// Mock`); solo la consulta de score vía Datacrédito no está mockeada. | `services/product/evaluations/src/third-party/Experian/*`, `services/product/evaluations/src/third-party/Datacredito/get-credit-score.ts`, `services/product/evaluations/src/routes.ts` |
| RF-011 | Rechazo automático por riesgo | Rechazar automáticamente una solicitud cuando la cuenta bancaria sea inválida, el score sea insuficiente o exista inconsistencia de datos. | Sistema (automático) | Alta | Implementado: el motor de reglas clasifica cada evaluación en `PASS / REVIEW / REJECTED`; si alguna regla dura falla, el resultado es `REJECTED` automáticamente, independiente del resultado de las reglas ponderadas. | `services/product/rules-engine/src/utils/evaluate-rule.ts`, `services/product/rules-engine/src/types.ts` |
| RF-012 | Decisión de aprobación y ajuste de cupo | Consultar el estado de crédito y aplicar las reglas del core bancario para decidir la aprobación o el ajuste del cupo. | Sistema (automático), analista de riesgo | Alta | Implementado (consulta) | `credit-line/get-credit-status.ts` |

### Originación del crédito

| ID | Nombre | Descripción | Actor(es) | Prioridad | Estado | Fuente |
|----|--------|--------------|-----------|-----------|--------|--------|
| RF-036 | Visualización y confirmación del cupo aprobado | Mostrar al cliente empresarial el valor de su cupo aprobado y las condiciones del crédito, exigiendo su confirmación explícita antes de continuar al plan de pagos y la firma del contrato. | Cliente empresarial | Alta | Implementado | `apps/redemption/app/onboarding/credit-conditions/page.tsx`, `apps/redemption/app/onboarding/layout.tsx` |
| RF-013 | Firma digital con proveedor externo | Firmar el contrato mediante el mecanismo de firma digital de un proveedor externo. | Cliente empresarial | Alta | Pendiente de confirmar con el equipo técnico el proveedor de firma digital vigente y su evidencia en el código; el flujo de `send-signature-otp.ts` documentado en versiones previas queda obsoleto según retroalimentación de negocio (ver HU-009). | `clients/sign-contract.ts`, `send-contract/send-contract.controller.ts` |
| RF-014 | Generación de contrato  | Generar el contrato en PDF a partir de una plantilla, y enviarlos por correo al cliente una vez firmados. | Cliente empresarial, sistema | Alta | Implementado | `clients/sign-contract.ts`, `send-contract/send-contract.controller.ts`, `backends/b2b/src/assets/contracts` |
| RF-015 | Activación del cupo y bono D1 | Activar el cupo y emitir el bono D1 una vez firmado el contrato, con fondeo a través de la fiducia del core bancario. | Sistema (automático) | Alta | No verificable, con precisión sobre el hallazgo: sí existe un mecanismo genérico de transición de estado de línea de crédito (`credit-line-status-update`, puede pasar a `active`) y webhooks de Druo, pero **no hay ningún concepto de "fiducia" en el código** (búsqueda exhaustiva sin resultados); la mecánica de fondeo vía fiducia del core bancario parece vivir fuera de este repositorio. | `services/core/credit-line-status-update/src/services/update-credit-line-status.service.ts` |

### Administración del crédito

| ID | Nombre | Descripción | Actor(es) | Prioridad | Estado | Fuente |
|----|--------|--------------|-----------|-----------|--------|--------|
| RF-016 | Consulta de estado y plan de pagos | Permitir consultar el estado del crédito, el saldo disponible y el plan de pagos vigente. | Cliente empresarial | Alta | Implementado | `credit-line/get-credit-status.ts`, `credit-line/simulate-payment-plan.ts` |
| RF-017 | Restricción de acceso por estado de crédito | Permitir el acceso al portal del cliente únicamente si la línea de crédito está en estado activa. | Sistema (automático) | Alta | Implementado | `apps/redemption/actions/auth.ts` |
| RF-018 | Ajuste administrativo de cupo y corte | Permitir al administrador ajustar el cupo y la fecha de corte de una línea de crédito, con las validaciones correspondientes. | Administrador del producto | Media | Implementado, con hallazgo: el rango válido de `cutoffDay` (0-31) no coincide con el exigido en redemption (1-31); se recomienda unificar. | `backends/admin/src/controllers/credit-lines.controller.ts`, `apps/redemption/lib/is-complete-redemption-credit-settings.ts` |

### Uso del crédito

| ID | Nombre | Descripción | Actor(es) | Prioridad | Estado | Fuente |
|----|--------|--------------|-----------|-----------|--------|--------|
| RF-019 | Canje mediante un codigo | Generar un código con tiempo de vida (TTL) para el canje del cupo en tienda D1. | Cliente empresarial | Alta | Implementado | ....|
| RF-020 | Canje mediante código de compra | Permitir revelar un código de compra como mecanismo alterno de canje del cupo. | Cliente empresarial | Alta | Implementado, con hallazgo: coexisten dos mecanismos de canje (código de compra) sin que la documentación de negocio aclare cuál es el vigente. | `clients/get-client-coupon.ts`, `apps/redemption/actions/reveal-purchase-code.ts` |
| RF-021 | Bloqueo y renovación del cupo | Bloquear el cupo remanente durante la compra y evaluar la renovación del cupo según el comportamiento de pago tras el uso. | Sistema (automático) | Alta | No verificable directamente en el código de `backends/b2b` disponible. | — |

### Gestión de pagos

| ID | Nombre | Descripción | Actor(es) | Prioridad | Estado | Fuente |
|----|--------|--------------|-----------|-----------|--------|--------|
| RF-022 | Cobro automático y prepago | Soportar el cobro automático de la cuota mediante Druo y el prepago voluntario por PSE. | Cliente empresarial, sistema | Alta | Parcialmente verificable: integración configurada con Druo; la ejecución del prepago por PSE no se encontró en el código disponible. | `backends/b2b/src/config/constants.ts` (`druo`), modelo `BankAccount` (`druoConnectionStatus`) |
| RF-023 | Reversión de desembolso | Eliminar un desembolso y restaurar automáticamente el cupo cuando el desembolso estaba activo. | Administrador del producto, sistema | Media | Implementado | `backends/admin/src/services/disbursements.service.ts` (`softDeleteDisbursement`) |
| RF-024 | Simulación de plan de pago | Permitir simular el plan de pago diario de un desembolso considerando tasa corriente, tasa de mora y umbral de días, con descarga en CSV. | Administrador del producto | Media | Implementado | `backends/admin/src/controllers/calculator.controller.ts`, `apps/admin/src/components/payment-plan-simulator.tsx` |

### Cobranza

| ID | Nombre | Descripción | Actor(es) | Prioridad | Estado | Fuente |
|----|--------|--------------|-----------|-----------|--------|--------|
| RF-025 | Registro de notas de cobranza | Permitir registrar notas de cobranza por cliente, incluyendo canal, dirección del contacto, resultado y monto de compromiso de pago. | Analista de cartera | Alta | Implementado; no descrito de forma explícita en el alcance de producto — se recomienda incorporarlo. | `backends/b2b/src/controllers/clients/collection-notes.ts` |
| RF-026 | Resumen de atención de cobranza | Permitir consultar un resumen de atención de cobranza por cliente, como insumo para el Comité de Cartera. | Analista de cartera, Comité de Cartera | Media | Implementado | `collection-notes.ts` (`getCollectionNotesAttentionSummary`) |
| RF-027 | Enforcement de blacklist | Restringir o bloquear operaciones (checkout, riesgo, desembolso) de clientes incluidos en la lista negra. | Sistema (automático) | Alta | Hallazgo: el catálogo existe (agregar/quitar cliente), pero no se encontró ningún punto donde se consulte antes de aprobar checkout, riesgo o desembolso. | `backends/b2b/src/controllers/blacklist/*.ts` |

### Servicio al cliente

| ID | Nombre | Descripción | Actor(es) | Prioridad | Estado | Fuente |
|----|--------|--------------|-----------|-----------|--------|--------|
| RF-028 | Atención de primer nivel por IA*| Permitir la atención de primer nivel mediante un asistente virtual y el escalamiento a un agente humano con el contexto completo de la conversación. | Cliente empresarial, asistente virtual (IA), agente humano | Alta | No verificable: no se encontró un módulo de asistente de IA para servicio al cliente en el repositorio; puede residir en una herramienta externa. | — |
| RF-029 | Validación de identidad en casos críticos | Requerir validación de identidad y aprobación manual explícita para casos críticos (suplantación, uso indebido del cupo, desconocimiento de compra). | Agente de servicio al cliente | Alta | No verificable directamente en el código disponible. | — |

### Portal administrativo

| ID | Nombre | Descripción | Actor(es) | Prioridad | Estado | Fuente |
|----|--------|--------------|-----------|-----------|--------|--------|
| RF-030 | Consulta de clientes y auditoría | Permitir buscar y consultar clientes por documento, incluyendo su historial de operaciones auditadas (línea de crédito, desembolsos, pagos), limitado a 500 filas. | Administrador del producto | Media | Implementado | `backends/admin/src/controllers/clients.controller.ts` (`getClientAuditedOperations`) |
| RF-031 | Registro de auditoría genérico | Registrar en un log de auditoría (`audit_log`) toda inserción, actualización o eliminación sobre las tablas de negocio del core, incluyendo el usuario que ejecuta el cambio. | Sistema (automático) | Alta | Implementado; funcionalidad clave para cumplimiento no mencionada en el alcance MVP conocido — se recomienda documentarla formalmente. | `runAuditedTransaction` (paquete `kernel`) |
| RF-032 | Administración de parámetros del producto | Permitir administrar parámetros configurables del producto (settings) por nombre, desde un panel restringido a administradores. | Administrador del producto | Media | Implementado | `backends/admin/src/controllers/settings.controller.ts` |
| RF-033 | Monitoreo del sistema | Permitir monitorear el estado del core bancario, la base de datos y servicios externos desde el portal administrativo, restringido a roles de sistema. | Administrador con rol de sistema | Media | Implementado parcialmente: el monitoreo de "terceros" cubre GitHub, npm y GCP, pero no los proveedores de negocio (Experian, Druo, biometría, Zenvia/Sendgrid, core bancario). | `system-core-health.controller.ts`, `system-cloud-sql.controller.ts`, `system-third-party-status.controller.ts` |

### Funcionalidades detectadas en el código sin requerimiento de negocio documentado

| ID | Nombre | Descripción | Actor(es) | Prioridad | Estado | Fuente |
|----|--------|--------------|-----------|-----------|--------|--------|
| RF-034 | Análisis financiero con IA * | Herramienta de análisis de estados financieros con IA presente en el flujo de checkout (ruta `/financial-analysis`). | Cliente empresarial (potencial) | Por definir | Sin requerimiento de negocio ni controlador backend confirmado; se recomienda validar con producto si está activa, en piloto o debe retirarse. | `apps/checkout/actions/financial-analysis` |
| RF-035 | Utilidades de datos de demostración | Endpoints y comportamientos especiales de restauración de datos de demostración, expuestos junto a funcionalidad de producto real. | Sistema (automático) | Por definir | Se recomienda moverlas fuera del código de producción o protegerlas explícitamente por ambiente. | `clients/restore-demo-client.ts`, `checkouts/update-checkout.ts` |

## Fuentes consultadas

- [Alcance del Producto](../../producto/alcance.md)
- [Reglas Negocio](../../negocio/reglas-negocio/README.md)
- [Procesos](../../negocio/procesos/README.md)
- Inventario funcional del código fuente `credits-platform-main`: `backends/b2b/src/controllers/*`, `backends/b2b/src/config/*`, `backends/b2b/src/db/models/*`, `backends/admin/src/controllers/*`, `backends/admin/src/services/*`, `apps/checkout`, `apps/redemption`, `apps/admin`, realizado como parte de esta actualización.
