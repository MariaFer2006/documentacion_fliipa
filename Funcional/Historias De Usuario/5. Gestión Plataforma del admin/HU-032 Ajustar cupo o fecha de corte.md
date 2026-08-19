#### HU-032: Ajustar cupo o fecha de corte

| Campo | Detalle |
|:---:|:---:|
| **Actor** | Administrador del producto |
| **Historia** | Como administrador, quiero ajustar el cupo o la fecha de corte de una línea de crédito, para corregir casos excepcionales autorizados por negocio. |
| **Prioridad** | Media |
| **Criterios de aceptación** | El administrador puede ajustar el cupo y el día de corte de una línea de crédito. El día de corte debe estar dentro del rango válido de **1 a 31**. La acción queda registrada en auditoría. |
| **Relaciones** | Casos de uso: CU-015. Requerimiento: RF-018. |
| **Referencias** | `backends/admin/src/controllers/credit-lines.controller.ts` — confirmado en `credits-platform-main`. |
 **Autor** | María Fernanda Herazo |
| **Fecha** | 18/08/2026 |
| **Versión** | V.1.7 |
| **Comentarios** | **Implementada.** Se confirma que, en la experiencia de usuario de **admin y portal**, el día de corte se maneja en el rango de **1 a 31**. A nivel interno, la API de administración aún admite el valor `0`, mientras que redemption exige `1–31`, lo que representa una discrepancia técnica entre módulos. Para negocio, el rango válido es **1–31**. |