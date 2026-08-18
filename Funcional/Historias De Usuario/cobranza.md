# Cobranza

[← Volver al índice](README.md)

Cubre el pago y recaudo del crédito (prepago por PSE, débito automático, alivios) y la gestión de cartera: segmentación por bucket de mora, registro de gestión de cobranza, tablero de priorización del Comité de Cartera y escalamiento jurídico.

**Historias en este capítulo:** HU-013 a HU-015, HU-024 a HU-027.

---

## Cliente empresarial / Sistema (Fliipa)

#### HU-013: Prepagar la cuota por PSE

| Campo | Detalle |
|:---:|:---:|
| **Actor** | Cliente empresarial |
| **Historia** | Como cliente empresarial, quiero prepagar mi cuota antes de la fecha de corte mediante PSE, para no incurrir en mora y mantener un buen comportamiento de crédito. |
| **Prioridad** | Alta |
| **Criterios de aceptación** | El cliente puede realizar el pago de su cuota en cualquier momento antes de la fecha de corte mediante PSE, y el sistema refleja el pago en su plan de pagos y en su cupo disponible. |
| **Relaciones** | Casos de uso: CU-011. Requerimiento: RF-022. Historia relacionada: HU-014. |
| **Referencias** | [Procesos](../negocio/procesos/08-cobro-pago.md); no se encontró implementación de pago por PSE en ningún archivo del repositorio (se buscó "PSE" en todo el proyecto sin coincidencias). |
| **Autor / Fecha / Versión** | María Fernanda Herazo |
| **Comentarios** | **Historia separada de la HU-009 original (v1.5)**, que combinaba prepago y débito automático en un solo paso; aunque ambos son pagos y ambos usan Druo, son procesos distintos que pertenecen a flujos diferentes. Se mantiene pendiente de confirmar con el equipo técnico si el prepago por PSE vive en un microservicio no incluido en este repositorio. |

#### HU-014: Débito automático de créditos vencidos

| Campo | Detalle |
|:---:|:---:|
| **Actor** | Sistema (Fliipa) |
| **Historia** | Como Fliipa, quiero debitar automáticamente los créditos que hayan superado su fecha de pago y aún presenten saldo pendiente por pagar, para asegurar el recaudo de la cartera vencida sin depender de una acción del cliente. |
| **Prioridad** | Alta |
| **Criterios de aceptación** | Un crédito es candidato a débito automático cuando: (1) superó la fecha de pago definida, (2) presenta saldo pendiente por pagar, (3) tiene una cuenta bancaria conectada y vigente en Druo, y (4) no está en un proceso de alivio o negociación activo que lo excluya. El sistema ejecuta el débito automáticamente vía Druo cuando se cumplen estas condiciones, y registra el resultado del intento (exitoso o fallido) mediante el webhook de eventos. |
| **Relaciones** | Casos de uso: CU-011. Requerimiento: RF-022. Historia relacionada: HU-013. |
| **Referencias** | `b2b/fliipa-back/src/services/druo/debit-bank-account.druo.ts`, `connect-bank-account.druo.ts`; `b2b/services/webhooks/src/controllers/webhooks/druo-events.webhook.ts` |
| **Autor / Fecha / Versión** | María Fernanda Herazo |
| **Comentarios** | **Historia separada de la HU-009 original (v1.5)**. El débito automático vía Druo sí está implementado (conexión de cuenta, débito, webhook de eventos). Se corrige el enfoque de la historia: el cliente no realiza ninguna acción (de hecho, está incumplido), por lo que no debe redactarse como "Como cliente" ni "Como cliente empresarial", sino como una historia de sistema ("Como Fliipa..."); los criterios de aceptación corresponden a las condiciones que hacen a un crédito candidato al débito automático, no a una acción del usuario. |

#### HU-015: Recibir alivios ante dificultades de pago

| Campo | Detalle |
|:---:|:---:|
| **Actor** | Cliente empresarial |
| **Historia** | Como cliente empresarial, quiero recibir alivios (abono parcial, congelamiento de intereses) cuando tengo dificultades temporales de pago, para no perder mi cupo ni mi historial. |
| **Prioridad** | Alta |
| **Criterios de aceptación** | El cliente puede acceder al abono parcial, congelamiento de intereses o condonación, según las condiciones y topes definidos por bucket de mora. |
| **Relaciones** | Casos de uso: CU-013. |
| **Referencias** | [Reglas Negocio](../negocio/reglas-negocio/03-alivios-negociacion.md) |
| **Autor / Fecha / Versión** | María Fernanda Herazo |
| **Comentarios** | No se encontró ningún módulo de alivios, condonación ni "bucket de mora" en el código revisado (se buscó "bucket", "mora", "condona*", "alivio*" en todo el repositorio; sin coincidencias relevantes — únicamente coincidencias de "bucket" de almacenamiento GCP, sin relación con cartera). Esta funcionalidad parece no estar implementada en el código fuente entregado, o vive en un sistema externo/manual. Se recomienda confirmar con negocio. |

## Analista de cartera / Comité de Cartera

#### HU-024: Ver cartera segmentada por bucket de mora

| Campo | Detalle |
|:---:|:---:|
| **Actor** | Analista de cartera |
| **Historia** | Como analista de cartera, quiero ver la cartera segmentada por bucket de mora, para priorizar mi gestión de cobro diaria. |
| **Prioridad** | Alta |
| **Criterios de aceptación** | El analista consulta la cartera agrupada en pago anticipado y buckets 1 a 5, con los datos necesarios para priorizar su gestión. |
| **Relaciones** | Casos de uso: CU-012. |
| **Referencias** | [Reglas Negocio](../negocio/reglas-negocio/02-mora-buckets.md) |
| **Autor / Fecha / Versión** | María Fernanda Herazo |
| **Comentarios** | El motor de reglas (`rules-engine`) que sí existe está enfocado en preaprobación, no en cobranza. Esta historia no está respaldada por el código fuente entregado; se recomienda validar si vive en un sistema externo de cobranza. Se mantiene la nota sobre la discrepancia de plazos de escalamiento documentada en RNF-017. |

#### HU-025: Registrar cada interacción de cobranza

| Campo | Detalle |
|:---:|:---:|
| **Actor** | Analista de cartera |
| **Historia** | Como analista de cartera, quiero registrar cada interacción de cobranza (canal, tipo de contacto, resultado, compromiso de pago), para mantener trazabilidad completa del caso. |
| **Prioridad** | Alta |
| **Criterios de aceptación** | El analista registra canal, tipo de contacto, resultado y monto comprometido de cada interacción, quedando disponible en el resumen de atención del cliente. |
| **Relaciones** | Casos de uso: CU-012. Requerimientos: RF-025, RF-026. Historia relacionada: HU-030 (capítulo [Servicio al cliente](servicio-cliente.md)). |
| **Referencias** | `b2b/fliipa-back/src/controllers/clients/collection-notes.ts` |
| **Autor / Fecha / Versión** | María Fernanda Herazo |
| **Comentarios** | **Confirmado**: el módulo está completamente implementado — creación, edición, eliminación y listado de notas de cobranza, más un resumen de atención (`getCollectionNotesAttentionSummary`). Ver HU-030 (nueva en v1.6) para el registro de contacto general, más allá de cobranza. |

#### HU-026: Tablero semanal de priorización del Comité de Cartera

| Campo | Detalle |
|:---:|:---:|
| **Actor** | Comité de Cartera |
| **Historia** | Como miembro del Comité de Cartera, quiero un tablero semanal con los casos priorizados (días de mora, monto, historial), para decidir alivios o escalamiento jurídico. |
| **Prioridad** | Alta |
| **Criterios de aceptación** | El comité visualiza semanalmente los casos priorizados según días de mora, flujo de caja, cuota vencida, historial y monto adeudado. |
| **Relaciones** | Casos de uso: CU-012, CU-013. |
| **Referencias** | [Reglas Negocio](../negocio/reglas-negocio/04-gestion-escalamiento.md) |
| **Autor / Fecha / Versión** | María Fernanda Herazo |
| **Comentarios** | Confirmado: no se encontró ningún tablero de priorización automatizado en el código revisado. Depende de la misma ausencia de lógica de mora/buckets señalada en HU-024. |

#### HU-027: Recibir casos de escalamiento jurídico automáticamente

| Campo | Detalle |
|:---:|:---:|
| **Actor** | Analista jurídico / abogado |
| **Historia** | Como analista jurídico, quiero recibir automáticamente los casos que llegan al bucket de escalamiento legal, para iniciar el proceso de cobro jurídico sin depender de un traspaso manual. |
| **Prioridad** | Media |
| **Criterios de aceptación** | Los casos que alcanzan el bucket de escalamiento jurídico se enrutan automáticamente al analista jurídico. |
| **Relaciones** | — |
| **Referencias** | [Actores](../negocio/Actores/03-actores-comerciales-cobranza.md) |
| **Autor / Fecha / Versión** | María Fernanda Herazo |
| **Comentarios** | Sin respaldo en código (consistente con la ausencia general de lógica de buckets de mora, ver HU-024). Depende de resolver primero la discrepancia de plazos de escalamiento (RNF-017). |

---

[← Anterior: KYC](kyc.md) · [Volver al índice](README.md) · [Siguiente: Servicio al cliente →](servicio-cliente.md)
