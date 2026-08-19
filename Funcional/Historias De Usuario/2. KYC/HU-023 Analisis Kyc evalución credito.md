
#### HU-023: Análisis de KYC + evaluación de crédito

| Campo | Detalle |
|:---:|:---:|
| **Actor** | Analista de riesgo |
| **Historia** | Como analista de riesgo, quiero ver en un solo lugar el resultado de Experian, el histórico transaccional de D1 y el score calculado, para validar o ajustar la decisión automática. |
| **Prioridad** | Alta |
| **Criterios de aceptación** | El analista consulta, para un cliente dado, el resultado de Experian, el histórico D1 y el score consolidado antes de aprobar o rechazar. |
| **Relaciones** | Casos de uso: CU-006. Requerimiento: RF-010. |
| **Referencias** | `b2b/fliipa-back/src/controllers/companies/lookup-company.ts`, `institutions/get-advance-score.ts`; `b2b/services/evaluations/src/third-party/Experian/*` |
 **Autor** | María Fernanda Herazo |
| **Fecha** | 18/08/2026 |
| **Versión** | V.1.7 |
| **Comentarios** | **Corrección v1.6**: se renombra el título de la historia (antes "Ver score, Experian e histórico D1 en un solo lugar") a "Análisis de KYC + evaluación de crédito", que refleja mejor el alcance funcional. La integración con Experian sí existe en el código (microservicio `evaluations`); lo que sigue sin encontrarse es una pantalla o endpoint que consolide en un solo lugar Experian + histórico D1 + score para el analista; cada dato se consulta por endpoints separados. Recomendamos aclarar si esa consolidación visual es responsabilidad del portal administrativo. |
