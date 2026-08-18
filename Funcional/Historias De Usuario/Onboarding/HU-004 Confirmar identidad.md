#### HU-004: Confirmar identidad

| Campo | Detalle |
|:---:|:---:|
| **Actor** | Cliente empresarial |
| **Historia** | Como cliente empresarial, quiero confirmar mi identidad mediante un código de verificación enviado por WhatsApp y por correo electrónico, para validar mi identidad de forma segura. |
| **Prioridad** | Alta |
| **Criterios de aceptación** | El cliente recibe el código OTP tanto por WhatsApp como por correo electrónico, lo ingresa en la plataforma y el sistema valida el código antes de permitirle continuar. Si la validación falla, el sistema muestra un mensaje genérico y no revela información sensible. |
| **Relaciones** | Casos de uso: CU-003. Requerimiento: RF-006. Historias relacionadas: HU-003, HU-005. |
| **Referencias** | `b2b/fliipa-back/src/controllers/otp/send-otp.ts`, `otp/validate-otp.ts` |
| **Autor / Fecha / Versión** | María Fernanda Herazo |
| **Comentarios** | la validación se realiza por los dos canales definidos (WhatsApp y correo electrónico), y no por "el canal autorizado"/"el canal definido" en singular como quedaba redactado hasta la v1.5. Pendiente confirmar con negocio si ambos canales son obligatorios o si basta con validar por uno de los dos. **Confirmado y ampliado (hallazgos técnicos vigentes)**: en `validate-otp.ts` existe un código comodín hardcodeado (`"490831"`, truncado según la longitud del código ingresado) que valida cualquier OTP — esto es el hallazgo de seguridad RNF-001. En `send-otp.ts` el canal `sms` no envía ningún mensaje real: solo registra una advertencia en consola (`console.warn("SMS channel not implemented yet")`) y responde `success: true` de forma simulada — esto confirma RNF-007. Ambos hallazgos son críticos y deben priorizarse antes de producción. |
