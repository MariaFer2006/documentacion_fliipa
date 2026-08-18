#### HU-022: Resolver manualmente casos de biometría en revisión

| Campo | Detalle |
|:---:|:---:|
| **Actor** | Analista de riesgo |
| **Historia** | Como analista de riesgo, quiero revisar manualmente los casos de biometría marcados "en revisión", para decidir si el cliente puede continuar el proceso. |
| **Prioridad** | Alta |
| **Criterios de aceptación** | El analista visualiza los casos "en revisión" y registra la decisión (continuar o rechazar). |
| **Relaciones** | Casos de uso: CU-005. Historia relacionada: HU-006 (capítulo [Onboarding](onboarding.md)). |
| **Referencias** | [Reglas Negocio](../../../Negocio/Reglas%20Negocio/07-kyc-evaluacion-riesgo.md); |
 **Autor** | María Fernanda Herazo |
| **Fecha** | 18/08/2026 |
| **Versión** | V.17 |
| **Comentarios** | No se encontró en el código ningún estado de "en revisión" para biometría, ni una cola o pantalla de revisión manual (se buscó "en_revision", "manual_review", "under_review" en todo el repositorio, sin coincidencias). Esta historia no tiene respaldo verificable en el código fuente entregado; se recomienda confirmar si el flujo de biometría vive en un sistema externo (proveedor de biometría) no incluido en este repositorio. |

https://github.com/MariaFer2006/documentacion_fliipa/blob/main/Negocio/Reglas%20Negocio/07-kyc-evaluacion-riesgo.md