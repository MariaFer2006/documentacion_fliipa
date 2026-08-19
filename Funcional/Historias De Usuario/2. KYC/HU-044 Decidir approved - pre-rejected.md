#### HU-044 — Decidir approved / pre_rejected y avisar cuando corresponda
| Campo | Detalle |
|:---:|:---:|
| **Actor** | Sistema (Fliipa) / operaciones (cierre final) |
| **Historia** | Como Fliipa, quiero aplicar el resultado del KYC al crédito (aprobado o pre-rechazado) y avisar al cliente solo cuando la decisión sea final, para que ops tenga cola clara y el cliente no reciba causas internas. |
| **Prioridad** | Alta |
| **Criterios de aceptación** | Si las 4 reglas pasan (Reconocer con warning = sigue pasando) → **approved** + correo de aceptación. Si falla una regla o cae el servicio de centrales → **pre_rejected** (cola ops + alerta), **sin** rechazo automático final y **sin** correo de rechazo en ese momento. Ops cierra a rejected o override a approved (ahí sí correo). Un fallo de servicio no se trata como aprobado. |
| **Relaciones** | [HU-008](../2.%20KYC/HU-008%20Conocer%20el%20resultado%20en%20m%C3%A1ximo%2024%20horas.md), [HU-011](../3.%20Credito/HU-011%20Ver%20mensaje%20de%20no%20disponibilidad%20de%20cr%C3%A9dito.md), [HU-041](../5.%20Gesti%C3%B3n%20Plataforma%20del%20admin/HU-041%20Cambiar%20el%20estado%20del%20cr%C3%A9dito%20(incluye%20pre-rechazado).md). (manual);  [HU-042](../2.%20KYC/HU-042%20%20Iniciar%20la%20evaluaci%C3%B3n%20KYC%20al%20quedar%20la%20solicitud%20en%20REQUESTED.md); [HU-043](../2.%20KYC/HU-043%20Evaluar%20reglas%20KYC.md), [HU-044](../2.%20KYC/HU-044%20Decidir%20approved%20-%20pre-rejected.md). |
| **Autor** | María Fernanda Herazo |
| **Fecha** | 18/08/2026 |
| **Versión** | V.1.7 |
| **Estado en plataforma** | **En desarrollo.** El cambio manual de estado ya existe (HU-041); se está implementando la decisión automática del motor y los correos de cierre. |
| **Comentarios** | Acuerdo de negocio: el motor no deja `rejected` automático; si no aprueba, va a `pre_rejected` (cola ops). |



