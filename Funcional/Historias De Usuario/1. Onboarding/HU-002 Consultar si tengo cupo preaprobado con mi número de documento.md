### HU-002: Consultar si tengo cupo preaprobado con mi número de documento

| Campo | Detalle |
|:---:|:---:|
| **Actor** | Cliente empresarial |
| **Historia** | Como cliente empresarial, quiero ingresar mi número de documento para consultar si tengo un cupo preaprobado, para decidir si continúo con el proceso de solicitud. |
| **Prioridad** | Alta |
| **Criterios de aceptación** | El cliente ingresa su número de Documento de Identidad. El sistema determina automáticamente el tipo de documento y consulta si existe una preaprobación asociada. El sistema informa al cliente si cuenta con una preaprobación y puede continuar con el proceso antes de completar el formulario de solicitud. |
| **Relaciones** | Casos de uso: CU-002. Historias relacionadas: HU-001, HU-003. |
| **Referencias** |[Procesos — 01 Onboarding Digital](../../../Operaciones/Procesos/01%20Onboarding%20Digital.md); `b2b/fliipa-back/src/controllers/checkouts/create-checkout.ts`|
| **Autor** | María Fernanda Herazo |
| **Fecha** | 18/08/2026 |
| **Versión** | v.1.7 |
| **Comentarios** | **Confirmado en plataforma:** el cliente ingresa su Documento de Identidad y el sistema determina si cuenta con una preaprobación y puede continuar con el proceso, antes de completar todo el formulario. Esta historia es distinta de HU-003: HU-002 valida la existencia de una preaprobación y determina si el cliente puede continuar; HU-003 corresponde a la visualización del valor del cupo preaprobado. |
