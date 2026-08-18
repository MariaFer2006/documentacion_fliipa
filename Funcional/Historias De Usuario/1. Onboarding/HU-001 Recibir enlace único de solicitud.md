
### HU-001: Recibir enlace único de solicitud

| Campo | Detalle |
|:---:|:---:|
| **Actor** | Cliente empresarial |
| **Historia** | Como cliente empresarial, quiero recibir un enlace único de solicitud por WhatsApp, para poder iniciar mi proceso de crédito de forma directa. |
| **Prioridad** | Alta |
| **Criterios de aceptación** | El cliente recibe por WhatsApp un enlace único asociado a su proceso de solicitud. Al acceder al enlace, el sistema valida el Documento de Identidad y, si ya existe una solicitud en estado `REQUEST_STARTED`, la reutiliza; si no existe una solicitud iniciada, crea una nueva. El hecho de que el cliente ya esté registrado no impide el ingreso al proceso. |
| **Relaciones** | Casos de uso: CU-001, CU-002. Historias relacionadas: HU-002, HU-003, HU-019. |
| **Referencias** | [Procesos](../negocio/procesos/01-captacion-comercial.md); `b2b/fliipa-back/src/controllers/checkouts/create-checkout.ts` |
| **Autor** | María Fernanda Herazo |
| **Fecha** | María Fernanda Herazo |
| **Versión** | María Fernanda Herazo |
| **Comentarios** | **Confirmado en plataforma:** al entrar con el enlace, el sistema valida el Documento de Identidad y, si ya existe una solicitud empezada en estado `REQUEST_STARTED`, la reutiliza; si no existe, crea una nueva. Que el cliente ya esté registrado no implica rechazar el ingreso. Para el equipo técnico: `create-checkout` reutiliza checkouts en estado `REQUEST_STARTED`; no existe un rechazo por el simple hecho de que ya exista un cliente asociado al documento. |
