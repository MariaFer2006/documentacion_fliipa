
#### HU-009: Firmar contrato mediante firma digital con proveedor externo

| Campo | Detalle |
|:---:|:---:|
| **Actor** | Cliente empresarial |
| **Historia** | Como cliente empresarial, quiero firmar mi contrato mediante firma digital con un proveedor externo, para activar mi cupo sin papeleo físico. |
| **Prioridad** | Alta |
| **Criterios de aceptación** | El cliente revisa el contrato y lo firma a través del mecanismo de firma digital del proveedor externo definido para este flujo. El sistema genera el PDF firmado y lo envía por correo al cliente. |
| **Relaciones** | Casos de uso: CU-007. Requerimientos: [RF-013](../../Requerimientos/Requerimientos%20Funcionales.md),[RF-014](../../Requerimientos/Requerimientos%20Funcionales.md), (pendiente confirmar vigencia dado el cambio de mecanismo). |
| **Referencias** | `b2b/fliipa-back/src/controllers/clients/sign-contract.ts`, `send-contract/send-contract.controller.ts` |
 **Autor** | María Fernanda Herazo |
| **Fecha** | 18/08/2026 |
| **Versión** | V.1.7 |
| **Comentarios** | **Corrección v1.6**: esta historia (antes HU-006, v1.5) ya no debe describir una firma por código OTP; según retroalimentación de negocio, ese flujo ya no ocurre y la firma se realiza mediante un proveedor externo de firma digital. Se retira la referencia a `send-signature-otp.ts`. Se recomienda que el equipo técnico confirme el proveedor de firma digital vigente y evalúe si `send-signature-otp.ts` debe retirarse del código para evitar mantener lógica obsoleta. |
