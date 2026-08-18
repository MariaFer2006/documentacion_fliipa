### HU-002: Consultar si tengo cupo preaprobado con mi número de documento

| Campo | Detalle |
|:---:|:---:|
| **Actor** | Cliente empresarial |
| **Historia** | Como cliente empresarial, quiero ingresar mi número de documento para consultar si tengo un cupo preaprobado, para decidir si continúo con el proceso de solicitud. |
| **Prioridad** | Alta |
| **Criterios de aceptación** | El cliente ingresa su tipo y número de documento y el sistema consulta si existe una preaprobación asociada. El sistema informa al cliente si puede continuar con el proceso antes de completar el formulario de solicitud. |
| **Relaciones** | Casos de uso: CU-002. Historias relacionadas: HU-001, HU-003. |
| **Referencias** | [Procesos](../negocio/procesos/02-onboarding-digital.md); `b2b/services/rules-engine/src/rule-models/b2b-base-preapproval.ts` |
| **Autor / Fecha / Versión** | María Fernanda Herazo |
| **Comentarios** | **Confirmado en plataforma:** el cliente ingresa su Documento de Identidad y el sistema determina si cuenta con una preaprobación y puede continuar con el proceso, antes de completar todo el formulario. Esta historia es distinta de HU-003: HU-002 valida la existencia de una preaprobación y determina si el cliente puede continuar; HU-003 corresponde a la visualización del valor del cupo preaprobado. |
