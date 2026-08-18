#### HU-004: Confirmar identidad

| Campo | Detalle |
|:---:|:---:|
| **Actor** | Cliente empresarial |
| **Historia** | Como cliente empresarial, quiero confirmar mi identidad mediante códigos de verificación enviados de forma secuencial por WhatsApp y correo electrónico, para validar mi identidad de forma segura. |
| **Prioridad** | Alta |
| **Criterios de aceptación** | El cliente recibe un código OTP por **WhatsApp** y, una vez completada y validada esta etapa, recibe el código OTP por **correo electrónico**. El cliente debe ingresar y validar cada código antes de continuar con el flujo. Si alguna validación falla, el sistema muestra un mensaje genérico y no revela información sensible. |
| **Relaciones** | Casos de uso: CU-003. Requerimiento: RF-006. Historias relacionadas: HU-003, HU-005. |
| **Referencias** | `b2b/fliipa-back/src/controllers/otp/send-otp.ts`, `otp/validate-otp.ts` |
 **Autor** | María Fernanda Herazo |
| **Fecha** | 18/08/2026 |
| **Versión** | V.17 |
| **Comentarios** | **Corrección funcional:** la validación de identidad se realiza mediante **dos OTP secuenciales**, no mediante códigos enviados simultáneamente. Primero se realiza la validación por WhatsApp y, una vez superada, se continúa con la validación por correo electrónico. La implementación debe respetar este orden y no permitir avanzar a la segunda etapa sin completar exitosamente la primera. **Hallazgos técnicos vigentes:** en `validate-otp.ts` existe un código comodín hardcodeado (`"490831"`, truncado según la longitud del código ingresado) que permite validar cualquier OTP; corresponde al hallazgo de seguridad RNF-001. En `send-otp.ts`, el canal `sms` no realiza un envío real: registra una advertencia mediante `console.warn("SMS channel not implemented yet")` y responde `success: true` de forma simulada; corresponde al hallazgo RNF-007. Estos hallazgos deben resolverse antes de producción. |