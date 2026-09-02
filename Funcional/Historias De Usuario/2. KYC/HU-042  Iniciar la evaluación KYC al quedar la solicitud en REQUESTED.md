#### HU-042 — Iniciar la evaluación KYC al quedar la solicitud en REQUESTED
| Campo | Detalle |
|:---:|:---:|
| **Actor** | Sistema (Fliipa) |
| **Historia** | Como Fliipa, quiero iniciar sola la evaluación KYC cuando el crédito pasa a REQUESTED (fin de onboarding, o cuando ops pide reevaluar / vuelve a REQUESTED), para no depender de que alguien dispare el motor a mano cada vez. |
| **Prioridad** | Alta |
| **Criterios de aceptación** | Al pasar a REQUESTED, el sistema dispara **una** corrida KYC (sin reintentos automáticos en loop). También se puede disparar desde ops ("Reevaluar KYC" o poner de nuevo REQUESTED). Si el disparo falla, queda registrado para ops y **no** se asume aprobación. |
| **Relaciones** | [HU-007](../2. KYC/HU-007 Cargar soportes bancarios.md), [HU-008](../2. KYC/HU-008 Conocer el resultado en m�ximo 24 horas.md), [HU-041](../5. Operaci�n admin/HU-041%20Cambiar%20el%20estado%20del%20cr%C3%A9dito%20%28incluye%20pre-rechazado%29.md) (cambio manual de estado); [HU-043](../2. KYC/HU-043 Evaluar reglas KYC.md), [HU-044](../2. KYC/HU-044 Decidir approved - pre-rejected.md).
. |
| **Autor** | María Fernanda Herazo |
| **Fecha** | 18/08/2026 |
| **Versión** | V.1.7 |
| **Estado en plataforma** | **En desarrollo.** El onboarding ya deja el crédito en REQUESTED y el motor de reglas ya existe; se está cableando el disparo automático de la corrida y el expediente de punta a punta. |
| **Comentarios** | Parte del motor KYC post-solicitud en curso. |





