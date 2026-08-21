#### HU-045: Visualización y confirmación del cupo aprobado

| Campo | Detalle |
|:---:|:---:|
| **Actor** | Cliente empresarial |
| **Historia** | Como cliente empresarial, quiero visualizar el monto de mi cupo aprobado y confirmarlo aceptando las condiciones de mi crédito, para continuar con el flujo de firma y disponibilización del crédito. |
| **Prioridad** | Alta |
| **Criterios de aceptación** | Una vez el cliente reingresa a la plataforma con una solicitud en estado Aprobado, el sistema le muestra de forma destacada el valor de su cupo aprobado junto con las condiciones del crédito (uso en tienda D1, plazo de pago, congelamiento por mora, entre otras). El cliente debe confirmar/aceptar dichas condiciones mediante un boton (Aceptar y continuar) para poder avanzar al siguiente paso del flujo (plan de pagos y firma de contrato). Si el cliente no confirma, no avanza en el flujo. |
| **Relaciones** | Casos de uso: [CU-026](../../Casos%20de%20Uso/3.%20Credito/CU-026%20Visualizar%20y%20confirmar%20el%20cupo%20aprobado.md). Requerimiento: [RF-036](../../Requerimientos/Requerimientos%20Funcionales.md). Historias relacionadas: [HU-023](../2.%20KYC/HU-023%20Analisis%20Kyc%20evaluci%C3%B3n%20credito.md), [HU-008](../2.%20KYC/HU-008%20Conocer%20el%20resultado%20en%20m%C3%A1ximo%2024%20horas.md), [HU-010](../3.%20Credito/HU-010%20Consultar%20cupo%2C%20plan%20de%20pagos%20y%20movimientos.md). |
| **Referencias** | `apps/redemption/app/onboarding/credit-conditions/page.tsx` (pantalla "Cupo aprobado" + botón "Aceptar condiciones"); `apps/redemption/app/onboarding/layout.tsx` (carga de `approvedCredit` desde `credit.lineCap`); `apps/redemption/actions/auth.ts` (redirección a `/onboarding` cuando `creditLineStatus.status === 'approved'`) |
| **Autor** | María Fernanda Herazo |
| **Fecha** | 20/08/2026 |
| **Versión** | V.1.0 |
| **Comentarios** | **Historia nueva, desprendida de HU-023 v1.7:** la visualización y confirmación del cupo aprobado por parte del cliente empresarial es un flujo distinto —con actor, pantalla y objetivo propios— del análisis de KYC y evaluación de crédito que realiza el analista de riesgo (HU-023). Mantenerlas juntas mezclaba dos actores y dos momentos del proceso distintos. Esta funcionalidad sí se encontró implementada en el código (`credit-conditions/page.tsx`), por lo que se documenta como **Implementado**. |
