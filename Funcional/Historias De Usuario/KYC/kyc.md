# KYC

[← Volver al índice](README.md)

Cubre el trabajo del analista de riesgo sobre los casos de biometría marcados en revisión y la consolidación del análisis de KYC con la evaluación de crédito. Las historias del cliente empresarial relacionadas con la captura de biometría y soportes bancarios (HU-006, HU-007) viven en el capítulo [Onboarding](onboarding.md); este capítulo cubre exclusivamente la revisión y evaluación por parte del analista de riesgo.

**Historias en este capítulo:** HU-022, HU-023.

---

## Analista de riesgo

#### HU-022: Resolver manualmente casos de biometría en revisión

| Campo | Detalle |
|:---:|:---:|
| **Actor** | Analista de riesgo |
| **Historia** | Como analista de riesgo, quiero revisar manualmente los casos de biometría marcados "en revisión", para decidir si el cliente puede continuar el proceso. |
| **Prioridad** | Alta |
| **Criterios de aceptación** | El analista visualiza los casos "en revisión" y registra la decisión (continuar o rechazar). |
| **Relaciones** | Casos de uso: CU-005. Historia relacionada: HU-006 (capítulo [Onboarding](onboarding.md)). |
| **Referencias** | [Reglas Negocio](../negocio/reglas-negocio/07-kyc-evaluacion-riesgo.md) |
| **Autor / Fecha / Versión** | María Fernanda Herazo |
| **Comentarios** | No se encontró en el código ningún estado de "en revisión" para biometría, ni una cola o pantalla de revisión manual (se buscó "en_revision", "manual_review", "under_review" en todo el repositorio, sin coincidencias). Esta historia no tiene respaldo verificable en el código fuente entregado; se recomienda confirmar si el flujo de biometría vive en un sistema externo (proveedor de biometría) no incluido en este repositorio. |

#### HU-023: Análisis de KYC + evaluación de crédito

| Campo | Detalle |
|:---:|:---:|
| **Actor** | Analista de riesgo |
| **Historia** | Como analista de riesgo, quiero ver en un solo lugar el resultado de Experian, el histórico transaccional de D1 y el score calculado, para validar o ajustar la decisión automática. |
| **Prioridad** | Alta |
| **Criterios de aceptación** | El analista consulta, para un cliente dado, el resultado de Experian, el histórico D1 y el score consolidado antes de aprobar o rechazar. |
| **Relaciones** | Casos de uso: CU-006. Requerimiento: RF-010. |
| **Referencias** | `b2b/fliipa-back/src/controllers/companies/lookup-company.ts`, `institutions/get-advance-score.ts`; `b2b/services/evaluations/src/third-party/Experian/*` |
| **Autor / Fecha / Versión** | María Fernanda Herazo |
| **Comentarios** | **Corrección v1.6**: se renombra el título de la historia (antes "Ver score, Experian e histórico D1 en un solo lugar") a "Análisis de KYC + evaluación de crédito", que refleja mejor el alcance funcional. La integración con Experian sí existe en el código (microservicio `evaluations`); lo que sigue sin encontrarse es una pantalla o endpoint que consolide en un solo lugar Experian + histórico D1 + score para el analista; cada dato se consulta por endpoints separados. Recomendamos aclarar si esa consolidación visual es responsabilidad del portal administrativo (ver hallazgo crítico en la conclusión del [README](README.md)). |

---

[← Anterior: Onboarding](onboarding.md) · [Volver al índice](README.md) · [Siguiente: Cobranza →](cobranza.md)
