# 3. Autenticación de clientes (checkout / redemption)

[← Volver al índice](README.md)

A diferencia del panel administrativo, los clientes empresariales (apps `checkout` y `redemption`) **no tienen roles ni permisos**: se autentican únicamente con documento (CC/CE/NIT) y PIN de 4 dígitos, y su sesión solo habilita el acceso a su propia información.

## Flujo de autenticación

1. El cliente envía documento, tipo de documento y PIN.
2. El sistema valida el formato del PIN (exactamente 4 dígitos) y del tipo de documento (`CC`, `CE` o `NIT`).
3. Se busca el cliente por documento + tipo de documento y se verifica el PIN contra el hash almacenado (`hashedPin`).
4. Si es correcto, se emite un JWT de sesión de corta duración.

## Bloqueo por intentos fallidos

| Parámetro | Valor |
|---|---|
| Intentos máximos | 3 |
| Duración del bloqueo | 24 horas |
| Activable/desactivable por configuración | `config.LOGIN_LOCKOUT_ENABLED` |

Si el cliente agota los intentos, la cuenta queda bloqueada por 24 horas desde el último intento fallido (`lockedAt`); el sistema calcula si el bloqueo ya expiró antes de permitir un nuevo intento.

## Duración de sesión

El JWT de sesión de un cliente autenticado normalmente expira en **2 minutos** (`JWT_EXPIRY = '2m'`). Esto es consistente con un patrón de sesión de corta duración renovada por el propio flujo de la aplicación, no con una sesión persistente de horas.

## Restricción de acceso por estado de crédito

El acceso al portal (`redemption`) está condicionado al estado de la línea de crédito del cliente:

- Si el estado es `approved`, el cliente es redirigido al flujo de onboarding de redemption (ver [HU-045](../Funcional/Historias De Usuario/2. KYC/HU-045 Visualizaci%C3%B3n%20y%20confirmaci%C3%B3n%20del%20cupo%20aprobado.md)).
- Solo los estados `approved` y `active` se consideran válidos para continuar en el portal (`isValidStatus`).
- El estado `preapproved` se maneja como un caso distinto dentro del flujo de autenticación.

## Referencias

`backends/b2b/src/services/login.ts`; `apps/redemption/actions/auth.ts`.