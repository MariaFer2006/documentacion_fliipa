# Historias de Usuario — Fliipa

| Documento | Historias Usuario |
|:---:|:---:|
| **Proyecto** | Fliipa |
| **Versión** | 1.7 |
| **Estado** | En revisión |
| **Responsable** | Producto y negocio |
| **Última actualización** | 2026-08-18 |

---

## Control de versiones

| Versión | Fecha | Autor | Descripción |
|:---:|:---:|:---:|:---:|
| 0.1 | 2026-07-06 | Maria Fernanda Herazo | Borrador vacío (pendiente de completar). |
| 1.0 | 2026-07-10 | María Fernanda Herazo | Primera versión completa: 28 historias de usuario por actor, en línea con Actores y Casos de Uso. |
| 1.1 | 2026-07-10 | María Fernanda Herazo | Se organizan las historias en tablas por actor, con prioridad y casos de uso relacionados. |
| 1.2 | 2026-07-10 | María Fernanda Herazo | Se convierte cada historia en una ficha individual (formato adaptado de plantilla de actor). |
| 1.3 | 2026-07-22 | Maria Fernanda Herazo | Se contrasta cada historia contra el código fuente real del repositorio `fliipa-main`. Se corrigen rutas de archivo inexactas y se marca como **hallazgo crítico** que el backend administrativo (`backends/admin`) referenciado en HU-024 a HU-028 no existe en el repositorio analizado. |
| 1.4 | 2026-07-30 | Maria Fernanda Herazo | Se corrige el hallazgo crítico de la v1.3: el repositorio de referencia correcto es `credits-platform-main`. Se corrigen las cinco fichas afectadas con rutas verificadas. |
| 1.5 | 2026-08-13 | María Fernanda Herazo | Revisión funcional y técnica integral: se elimina la referencia a "tendero", se unifica el repositorio de referencia en `credits-platform-main`, se corrige el SLA a 24 horas, se precisa la validación por OTP y se matiza la referencia a Datacrédito. |
| 1.6 | 2026-08-13 | María Fernanda Herazo | Revisión funcional integral a partir de retroalimentación de negocio (24 observaciones): se agrega HU-002 y se renumeran todas las historias subsecuentes (36 historias, HU-001 a HU-036); se separan historias no atómicas (biometría/soportes, prepago/débito, IA/escalamiento humano); se corrigen criterios de aceptación redactados como precondiciones; se agregan historias faltantes (reintento de OTP, clientes sin oferta de crédito, registro general de contacto, consulta de blacklist, motivo de ingreso a blacklist). |
| **1.7** | **2026-08-18** | María Fernanda Herazo | **Reestructuración documental** (decisión de la reunión Weekly Sync del 2026-08-14): se abandona el archivo único y las 36 historias se organizan en capítulos por vertical de servicio: [Onboarding](onboarding.md), [KYC](kyc.md), [Cobranza](cobranza.md), [Servicio al cliente](servicio-cliente.md) y [Administración](administracion.md). El contenido de cada ficha (identificador, criterios de aceptación, referencias, comentarios) se conserva sin cambios respecto a la v1.6; solo cambia su ubicación y agrupación. Este README pasa a ser el punto de entrada y conserva el control de versiones, el objetivo, el alcance y la conclusión de la revisión funcional. |

---

## Objetivo

Describir las necesidades de cada actor de Fliipa en lenguaje de negocio, como base para la priorización y el desarrollo de las funcionalidades del sistema.

## Alcance

Cubre historias de usuario para el cliente empresarial, el asesor comercial, el analista de riesgo, el analista de cartera, el agente de servicio al cliente y el administrador del producto, en línea con los actores descritos en [Actores](../negocio/Actores/README.md) y los casos de uso en [Casos De Uso](casos-de-uso.md). Usa la numeración `HU-XXX` definida en [Convenciones](../CONVENCIONES.md).

## Contenido

Cada historia se documenta como una ficha individual: identificador, descripción, criterios de aceptación, relaciones con otros elementos del desarrollo, referencias de origen, control de autor/fecha/versión y comentarios adicionales. Los campos "Referencias" y "Comentarios" fueron verificados directamente contra el código fuente en la revisión v1.3-1.5; las historias nuevas o reformuladas de la v1.6 provienen de retroalimentación de negocio y se marcan explícitamente como pendientes de verificación en código donde corresponda.

A partir de la v1.7, el documento se organiza en capítulos por vertical de servicio en lugar de un único archivo. La numeración global `HU-001` a `HU-036` se mantiene sin cambios entre capítulos para preservar la trazabilidad con Casos de Uso, Requerimientos y el código fuente.

### Índice de capítulos

| Capítulo | Contenido | Historias |
|:---|:---|:---:|
| [Onboarding](onboarding.md) | Solicitud, consulta y visualización de cupo, validación de identidad (OTP), biometría, carga de soportes, resultado de la solicitud, firma de contrato, primer uso del cupo, recuperación de PIN, y la gestión comercial que acompaña el proceso (contacto multicanal, acompañamiento del asesor, seguimiento a clientes sin primera compra). | HU-001 a HU-012, HU-018 a HU-021 |
| [KYC](kyc.md) | Revisión manual de casos de biometría y consolidación del análisis de riesgo/crédito por parte del analista de riesgo. | HU-022, HU-023 |
| [Cobranza](cobranza.md) | Pagos (PSE, débito automático), alivios, segmentación de cartera por mora, registro de gestión de cobranza, tablero del Comité de Cartera y escalamiento jurídico. | HU-013 a HU-015, HU-024 a HU-027 |
| [Servicio al cliente](servicio-cliente.md) | Atención por asistente virtual con IA, escalamiento a agente humano, validación de identidad en casos críticos y registro general de todo contacto con el cliente. | HU-016, HU-017, HU-028 a HU-030 |
| [Administración](administracion.md) | Portal administrativo: búsqueda de clientes e historial auditado, ajustes de cupo/fecha de corte, simulador de plan de pago, administración de blacklist y monitoreo de salud del sistema. | HU-031 a HU-036 |

> **Nota:** algunas historias tienen relaciones que cruzan capítulos (por ejemplo, HU-006/HU-007 de Onboarding con HU-022 de KYC, o HU-011 de Onboarding con HU-034/HU-035 de Administración). El campo "Relaciones" de cada ficha indica explícitamente estos cruces; no se duplica el contenido de la historia entre capítulos.

## Conclusión de la revisión (v1.6)

La revisión funcional de la versión v1.6 incorporó 24 observaciones de negocio identificadas sobre la v1.5, tomando como referencia el documento fuente de retroalimentación. Los principales cambios fueron:

- Incorporación de una historia previa a la consulta de cupo, lo que implicó la renumeración de las historias posteriores.
- Separación de historias no atómicas en historias independientes, particularmente en los flujos de biometría y soportes bancarios, prepago y débito automático, y atención mediante IA y atención humana.
- Corrección de criterios de aceptación que correspondían a precondiciones, pasos del proceso o mecanismos operativos, en lugar de condiciones verificables para determinar el cumplimiento de la historia.
- Eliminación de restricciones no justificadas que limitaban el flujo exclusivamente al uso del celular.
- Incorporación de historias faltantes, entre ellas el reintento de OTP, la gestión de clientes sin oferta de crédito, el registro general de contactos, la consulta de blacklist y el registro del motivo de ingreso a blacklist.

Se mantienen vigentes los hallazgos técnicos identificados en versiones anteriores, entre ellos el uso de un OTP comodín, el canal SMS simulado, la ausencia en el repositorio de módulos correspondientes a biometría, alivios, mora por buckets e IA conversacional, así como la falta de enforcement de la blacklist. Estos aspectos deberán ser revisados y priorizados conjuntamente por negocio y el equipo técnico antes de llevar las historias a desarrollo.

### Tabla de correspondencia de numeración (v1.5 → v1.6)

| v1.5 | v1.6 | Cambio |
|:---:|:---:|:---|
| HU-001 | HU-001 | Sin cambios de contenido. |
| — | **HU-002** | Nueva: consultar cupo preaprobado por documento. |
| HU-002 | HU-003 | Renumerada. |
| HU-003 | HU-004 | Actualizada: validación por WhatsApp y correo. |
| — | **HU-005** | Nueva: reintento/corrección de OTP. |
| HU-004 | HU-006 + HU-007 | Dividida en biometría y soportes bancarios. |
| HU-005 | HU-008 | Renumerada. |
| HU-006 | HU-009 | Reescrita: firma digital con proveedor externo. |
| HU-007 | HU-010 | Renumerada. |
| — | **HU-011** | Nueva: mensaje de no disponibilidad de crédito. |
| HU-008 | HU-012 | Renumerada. |
| HU-009 | HU-013 + HU-014 | Dividida en prepago (PSE) y débito automático (Fliipa). |
| HU-010 | HU-015 | Renumerada. |
| HU-011 | HU-016 + HU-017 | Dividida en atención IA y escalamiento a humano. |
| HU-012 | HU-018 | Corrección tipográfica. |
| HU-013 | HU-019 | Corrección de criterio de aceptación (precondición → resultado). |
| HU-014 | HU-020 | Renumerada. |
| HU-015 | HU-021 | Corrección de título y criterios de aceptación. |
| HU-016 | HU-022 | Renumerada. |
| HU-017 | HU-023 | Renombrada: "Análisis de KYC + evaluación de crédito". |
| HU-018 | HU-024 | Renumerada. |
| HU-019 | HU-025 | Renumerada. |
| HU-020 | HU-026 | Renumerada. |
| HU-021 | HU-027 | Renumerada. |
| HU-022 | HU-028 | Renumerada. |
| HU-023 | HU-029 | Renumerada. |
| — | **HU-030** | Nueva: registro general de contacto con el cliente. |
| HU-024 | HU-031 | Renumerada. |
| HU-025 | HU-032 | Renumerada. |
| HU-026 | HU-033 | Renumerada. |
| HU-027 | HU-034 | Actualizada: registro de motivo de ingreso a blacklist. |
| — | **HU-035** | Nueva: consultar clientes en blacklist. |
| HU-028 | HU-036 | Renumerada. |

## Fuentes consultadas

- [Actores](../negocio/Actores/README.md)
- [Procesos](../negocio/procesos/README.md)
- [Reglas Negocio](../negocio/reglas-negocio/README.md)
- [Casos De Uso](casos-de-uso.md)
- [Requerimientos Funcionales](requerimientos-funcionales.md)
- [Requerimientos No Funcionales](requerimientos-no-funcionales.md)
- Inventario funcional del código fuente `credits-platform-main` (base de la v1.0-1.2).
- Revisión directa del código fuente del repositorio `credits-platform-main.zip`, realizada como parte de la corrección v1.4. Este es el repositorio de código de referencia vigente.
- Documento de retroalimentación funcional de negocio sobre la versión 1.5 (24 observaciones numeradas), base de los cambios incorporados en la v1.6.
- Acta y transcripción de la reunión Weekly Sync del 2026-08-14, base de la reestructuración documental de la v1.7.
