#### HU-044 — Decidir approved / pre_rejected y avisar cuando corresponda
| Campo | Detalle |
|:---:|:---:|
| **Actor** | Sistema (Fliipa) / operaciones (cierre final) |
| **Historia** | Como Fliipa, quiero aplicar el resultado del KYC al crédito (aprobado o pre-rechazado) y avisar al cliente solo cuando la decisión sea final, para que ops tenga cola de solicitudes y el cliente no reciba causas internas. |
| **Prioridad** | Alta |
| **Criterios de aceptación** | Si las 4 reglas pasan (Reconocer con warning = sigue pasando) → **approved** + correo de aceptación. Si falla una regla o cae el servicio de centrales → **pre_rejected** (cola ops + alerta), **sin** rechazo automático final y **sin** correo de rechazo en ese momento. Ops cierra a rejected o override a approved (ahí sí correo). Un fallo de servicio no se trata como aprobado. |
| **Relaciones** | [HU-008](../2. KYC/HU-008 Conocer el resultado en m�ximo 24 horas.md), [HU-011](../3. Credito/HU-011 Ver mensaje de no disponibilidad de cr�dito.md), [HU-041](../5. Operaci�n admin/HU-041%20Cambiar%20el%20estado%20del%20cr%C3%A9dito%20%28incluye%20pre-rechazado%29.md). (manual);  [HU-042](../2. KYC/HU-042  Iniciar la evaluaci�n KYC al quedar la solicitud en REQUESTED.md); [HU-043](../2. KYC/HU-043 Evaluar reglas KYC.md), [HU-044](../2. KYC/HU-044 Decidir approved - pre-rejected.md). |
| **Autor** | María Fernanda Herazo |
| **Fecha** | 18/08/2026 |
| **Versión** | V.1.7 |
| **Estado en plataforma** | **En desarrollo.** El cambio manual de estado ya existe (HU-041); se está implementando la decisión automática del motor y los correos de cierre. |
| **Comentarios** | Acuerdo de negocio: el motor no deja `rejected` automático; si no aprueba, va a `pre_rejected` (cola ops). |



