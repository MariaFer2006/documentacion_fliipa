#### HU-044 — Decidir approved / pre_rejected y avisar cuando corresponda
| Campo | Detalle |
|:---:|:---:|
| **Actor** | Sistema (Fliipa) / operaciones (cierre final) |
| **Historia** | Como Fliipa, quiero aplicar el resultado del KYC al crédito (aprobado o pre-rechazado) y avisar al cliente solo cuando la decisión sea final, para que ops tenga cola clara y el cliente no reciba causas internas. |
| **Prioridad** | Alta |
| **Criterios de aceptación** | Si las 4 reglas pasan (Reconocer con warning = sigue pasando) → **approved** + correo de aceptación. Si falla una regla o cae el servicio de centrales → **pre_rejected** (cola ops + alerta), **sin** rechazo automático final y **sin** correo de rechazo en ese momento. Ops cierra a rejected o override a approved (ahí sí correo). Un fallo de servicio no se trata como aprobado. |
| **Relaciones** | HU-008, HU-011, HU-041 (manual); HU-042; HU-043. |
| **Autor** | María Fernanda Herazo |
| **Fecha** | 18/08/2026 |
| **Versión** | V.1.7 |
| **Estado en plataforma** | **En desarrollo.** El cambio manual de estado ya existe (HU-041); se está implementando la decisión automática del motor y los correos de cierre. |
| **Comentarios** | Acuerdo de negocio: el motor no deja `rejected` automático; si no aprueba, va a `pre_rejected` (cola ops). |
