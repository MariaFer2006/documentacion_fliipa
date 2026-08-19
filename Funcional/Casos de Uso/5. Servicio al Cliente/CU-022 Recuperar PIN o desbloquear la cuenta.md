### CU-022: Recuperar PIN o desbloquear la cuenta

![Diagrama de caso de uso CU-022](imagenes/diagrama_CU-022.svg)

> **Nota:** HU-018 no traía un número de CU asignado (solo referenciaba el requerimiento RNF-014); se asigna el consecutivo **CU-022**.

| Campo | Detalle |
|---|---|
| **Actores** | Cliente empresarial; Agente de servicio al cliente |
| **Descripción** | El cliente recupera su PIN cuando lo olvida, o desbloquea su cuenta cuando queda bloqueada, comunicándose con soporte, para no perder el acceso a su cupo. |
| **Precondiciones** | El cliente olvidó su PIN, o su cuenta quedó bloqueada tras varios intentos fallidos de acceso. |
| **Flujo principal** | 1. El cliente se comunica con soporte indicando que olvidó su PIN o que su cuenta está bloqueada.<br>2. El agente de servicio al cliente verifica la situación de la cuenta (intentos de acceso, bloqueo).<br>3. El agente ayuda al cliente a generar un nuevo PIN o a desbloquear la cuenta.<br>4. El cliente recupera el acceso a su cupo. |
| **Flujos alternativos / excepciones** | A1. El cliente no puede verificarse ante soporte: el desbloqueo no procede hasta resolver la verificación de identidad. |
| **Postcondiciones** | El cliente recupera el acceso a su cuenta con un PIN válido. |
| **Reglas de negocio** | El desbloqueo y la generación de un nuevo PIN requieren pasar por soporte; no es un autoservicio del cliente. |
| **Historias de usuario relacionadas** | HU-018 (Recuperar PIN o desbloquear la cuenta) |
| **Estado en plataforma** | Implementado. Existe el modelo con `loginAttempts`/`lockedAt` (`Client.ts`) y un componente de UI dedicado (`ResetPin.tsx`) dentro del flujo de login de `fliipa-redemption`. |
| **Referencias** | Fuente: ficha HU-018 — *Historias de Usuario — Fliipa*, carpeta "5. Servicio al Cliente" (repositorio `documentacion_fliipa`, María Fernanda Herazo). |
