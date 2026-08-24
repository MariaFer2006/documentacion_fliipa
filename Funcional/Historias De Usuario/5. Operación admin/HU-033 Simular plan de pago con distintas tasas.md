#### HU-033: Simular plan de pago con distintas tasas

| Campo | Detalle |
|:---:|:---:|
| **Actor** | Administrador del producto |
| **Historia** | Como administrador, quiero simular el plan de pago de un cliente con distintas tasas, para preparar acuerdos de pago o alivios. |
| **Prioridad** | Media |
| **Criterios de aceptación** | El administrador ingresa tasa corriente, tasa de mora , y obtiene el plan de pago diario descargable en CSV. |
| **Relaciones** | Casos de uso: [CU-016](../../Casos%20de%20Uso/6.%20Operaci%C3%B3n%20Admin/CU-016%20Simular%20plan%20de%20pago%20con%20distintas%20tasas.md). Requerimiento:[RF-024](../../Requerimientos/Requerimientos%20Funcionales.md). |
| **Referencias** | `backends/admin/src/controllers/calculator.controller.ts` (`getCalculatorStatus`, recibe `currentInterestRate`, `overdueInterestRate`, `thresholdDays`); descarga CSV en `apps/admin/src/lib/generate-csv-file.ts` y `apps/admin/src/app/disbursements/consult/CalculatorDownloaderButton.tsx` — confirmado en `credits-platform-main`. |
 **Autor** | María Fernanda Herazo |
| **Fecha** | 18/08/2026 |
| **Versión** | V.1.7 |
| **Comentarios** | Implementada, exactamente con los campos descritos en la historia (tasa corriente, tasa de mora) y con descarga CSV real. |
