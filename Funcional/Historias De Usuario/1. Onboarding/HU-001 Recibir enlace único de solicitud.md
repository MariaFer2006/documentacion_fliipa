#### HU-001: Recibir enlace único de solicitud
| Campo | Detalle |
|:---:|:---:|
| **Actor** | Cliente empresarial |
| **Historia** | Como cliente empresarial, quiero recibir un enlace único de solicitud por WhatsApp, para poder iniciar mi proceso de crédito de forma directa. |
| **Prioridad** | Alta |
| **Criterios de aceptación** | El cliente recibe por WhatsApp un enlace único asociado a su proceso de solicitud. Al acceder al enlace, el sistema valida el Documento de Identidad y, si ya existe una solicitud en estado `REQUEST_STARTED`, la reutiliza; si no existe una solicitud iniciada, crea una nueva. El hecho de que el cliente ya esté registrado no impide el ingreso al proceso. |
| **Relaciones** | Casos de uso: CU-001, CU-002. Historias relacionadas: [HU-002](../1.%20Onboarding/HU-002%20Consultar%20si%20tengo%20cupo%20preaprobado%20con%20mi%20n%C3%BAmero%20de%20documento.md), [HU-003](../1.%20Onboarding/HU-003%20Ver%20cupo%20preaprobado%20antes%20de%20completar%20el%20formulario.md), [HU-019](../1.%20Onboarding/HU-019%20Contacto%20simult%C3%A1neo%20multicanal.md). |
| **Referencias** | [Procesos — 01 Onboarding Digital](../../../Operaciones/Procesos/01%20Onboarding%20Digital.md); `b2b/fliipa-back/src/controllers/checkouts/create-checkout.ts` |
| **Autor** | María Fernanda Herazo |
| **Fecha** | 18/08/2026 |
| **Versión** | v.1.7 |
| **Comentarios** | **Confirmado en plataforma:** al entrar con el enlace, el sistema valida el Documento de Identidad y, si ya existe una solicitud empezada en estado `REQUEST_STARTED`, la reutiliza; si no existe, crea una nueva. Que el cliente ya esté registrado no implica rechazar el ingreso. Para el equipo técnico: `create-checkout` reutiliza checkouts en estado `REQUEST_STARTED`; no existe un rechazo por el simple hecho de que ya exista un cliente asociado al documento. |

