
### HU-005: Reintentar o corregir el envío del OTP

| Campo | Detalle |
|:---:|:---:|
| **Actor** | Cliente empresarial |
| **Historia** | Como cliente empresarial, quiero poder reintentar el envío del código OTP cuando no me llega, o corregir mi número de teléfono o correo si los ingresé mal, para poder completar la validación de identidad. |
| **Prioridad** | Alta |
| **Criterios de aceptación** | El cliente puede solicitar nuevamente el envío del código OTP cuando no lo recibe, respetando el tiempo de espera definido entre envíos. Si el cliente ingresó incorrectamente su número de teléfono o correo electrónico, puede regresar al paso anterior, corregir el dato y solicitar un nuevo código sin reiniciar toda la solicitud. El nuevo código se envía al dato de contacto corregido. |
| **Relaciones** | Casos de uso: CU-003. Historia relacionada: [HU-004](../1.%20Onboarding/HU-004%20Confirmar%20identidad.md). |
| **Referencias** | `b2b/fliipa-back/src/controllers/otp/send-otp.ts`, `otp/validate-otp.ts` |
 **Autor** | María Fernanda Herazo |
| **Fecha** | 18/08/2026 |
| **Versión** | V.1.7 |
| **Comentarios** | **Confirmado en plataforma:** el cliente puede solicitar nuevamente el código OTP y existe un tiempo de espera entre envíos. Si el número de teléfono o correo fue ingresado incorrectamente, el cliente puede regresar al paso anterior, corregir el dato y solicitar un nuevo código sin reiniciar la solicitud desde cero. |
