#### HU-018: Recuperar PIN o desbloquear la cuenta

| Campo | Detalle |
|:---:|:---:|
| **Actor** | Cliente empresarial |
| **Historia** | Como cliente empresarial, quiero recuperar mi PIN si lo olvido o mi cuenta se bloquea, para no perder el acceso a mi cupo. |
| **Prioridad** | Media |
| **Criterios de aceptación** | El cliente debe comunicarse con soporte para recibir ayuda y generar un nuevo PIN. |
| **Relaciones** | Casos de uso: [CU-022](../../Casos%20de%20Uso/5.%20Servicio%20al%20Cliente/CU-022%20Recuperar%20PIN%20o%20desbloquear%20la%20cuenta.md) (recuperar PIN), [CU-027](../../Casos%20de%20Uso/5.%20Servicio%20al%20Cliente/CU-027%20Desbloquear%20la%20cuenta.md) (desbloquear cuenta). Requerimiento: [RFN-014](../../Requerimientos/Requerimientos%20No%20Funcionales.md). (bloqueo de acceso). |
| **Referencias** | `b2b/fliipa-back/src/db/models/Client.ts` (`loginAttempts`, `lockedAt`); `b2b/fliipa-redemption/components/pages/login/ResetPin.tsx` |
 **Autor** | María Fernanda Herazo |
| **Fecha** | 18/08/2026 |
| **Versión** | V.1.8 |
| **Comentarios** | **Corrección v1.6**: se corrige error tipográfico ("Soporto" → "soporte") en el criterio de aceptación. **Confirmado y ampliado**: además del modelo con `loginAttempts`/`lockedAt`, existe un componente de UI dedicado (`ResetPin.tsx`) dentro del flujo de login de `fliipa-redemption`. **Corrección v1.8 (2026-08-28):** en el catálogo de Casos de Uso, CU-022 se dividió en dos fichas: [CU-022](../../Casos%20de%20Uso/5.%20Servicio%20al%20Cliente/CU-022%20Recuperar%20PIN%20o%20desbloquear%20la%20cuenta.md) (recuperar PIN) y [CU-027](../../Casos%20de%20Uso/5.%20Servicio%20al%20Cliente/CU-027%20Desbloquear%20la%20cuenta.md) (desbloquear la cuenta), ya que son disparadores distintos. Esta historia (HU-018) sigue cubriendo ambos casos de uso hasta que se decida dividirla también a nivel de historia de usuario. |