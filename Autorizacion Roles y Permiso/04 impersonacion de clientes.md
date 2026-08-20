# 4. Impersonación de clientes ("entrar como usuario")

[← Volver al índice](README.md)

El panel administrativo permite a un usuario con el permiso `product:impersonate-client` iniciar sesión en el portal del cliente (`redemption`) **como si fuera ese cliente**, sin conocer su PIN. El mecanismo está diseñado como un intercambio de tokens de corta duración entre tres servicios: `admin` → `b2b` → `redemption`.

## Flujo completo

1. **Admin panel → backend admin:** un usuario con permiso `product:impersonate-client` solicita `POST /product/clients/:id/impersonate`. Se registra la acción en el log de auditoría (`admin_action_log`, acción `client.impersonate`), incluyendo intentos fallidos.
2. **Backend admin → b2b (interno):** el backend admin llama internamente a `b2b: POST /auth/impersonate`, autenticado con un secreto compartido (`X-Internal-Secret` / `IMPERSONATE_INTERNAL_SECRET`), enviando `clientId`, `adminUserId` y `adminEmail`.
3. **Validación de elegibilidad:** `b2b` verifica que la línea de crédito del cliente esté en estado `approved` o `active` (`IMPERSONATION_ALLOWED_STATUSES`); si no, rechaza la impersonación.
4. **b2b emite un token de intercambio** (`exchangeToken`), de propósito único (`impersonate_exchange`), válido por **60 segundos**, con un `jti` (identificador único) para trazabilidad.
5. **Admin redirige al usuario** a `redemption` con ese `exchangeToken` en la URL (`/auth/impersonate?token=...`).
6. **Redemption → b2b:** `redemption` intercambia el token por una sesión real llamando a `POST /auth/impersonate/exchange`.
7. **b2b emite un JWT de sesión** de cliente, válido por **10 minutos** (`SESSION_TTL`), que incluye además `impersonatedBy` e `impersonatedByName` — es decir, la sesión resultante queda marcada como impersonada, con el correo y nombre del administrador que la originó.

## Reglas de negocio relevantes

- Solo se puede impersonar a clientes con línea de crédito **aprobada o activa**; no se puede impersonar a un cliente rechazado, en revisión o sin solicitud.
- El token de intercambio es de un solo uso funcional y expira en 60 segundos: no está pensado para reutilizarse ni para persistir.
- La sesión resultante de la impersonación (10 minutos) es más corta que el ciclo normal de uso del portal, y queda explícitamente marcada como impersonada en el JWT.
- Toda impersonación (exitosa o fallida) se registra en el log de auditoría del panel admin, incluyendo el identificador del cliente.

## Pendiente detectado en el código

El envío de una alerta operativa (`sendOperationalAlert`) por cada impersonación —que notificaría por canal interno cuando un administrador entra como un cliente— está **comentado/deshabilitado** en `impersonate.service.ts` (bloque de código presente pero inactivo). Se recomienda confirmar con el equipo si esta alerta debe reactivarse por trazabilidad y control interno.

## Referencias

`backends/b2b/src/services/impersonate.service.ts`; `backends/b2b/src/controllers/auth/impersonate.ts`; `backends/b2b/src/routes.ts`; `backends/admin/src/controllers/product-impersonate.controller.ts`; `backends/admin/src/routes.ts`.