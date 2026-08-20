# 2. Matriz de permisos por acción

[← Volver al índice](README.md)

Cada permiso es un *slug* (`PermissionSlug`) agrupado en dos familias: `core:*` (administración del crédito/core bancario) y `product:*` (gestión de producto sobre datos del cliente). Un usuario tiene los permisos base de su rol (ver [01](01%20Roles%20del%20Panel%20Administrativo.md)) más cualquier permiso individual otorgado en `extra_permissions`.

## Permisos `core:*`

| Slug | Etiqueta (panel) |
|---|---|
| `core:create-user` | Crear usuarios |
| `core:update-user` | Editar usuarios |
| `core:delete-user` | Eliminar usuarios |
| `core:read-user-activity` | Ver actividad de usuarios |
| `core:reset-user-password` | Restablecer contraseña |
| `core:update-line-cap` | Modificar cupo de línea |
| `core:update-cutoff-day` | Modificar día de corte |
| `core:update-status` | Modificar estado de línea |
| `core:get-client-history` | Ver historial de cliente |
| `core:simulate-payment-plan` | Simular plan de pagos |
| `core:add-disbursement` | Agregar desembolso |
| `core:register-payment` | Registrar pago |
| `core:delete-disbursement` | Eliminar desembolso |
| `core:get-calculator` | Usar calculadora (consulta) |
| `core:download-calculator` | Descargar calculadora |
| `core:update-setting` | Editar configuración |
| `core:download-credits-report` | Descargar reporte de créditos |
| `core:download-payments-report` | Descargar reporte de pagos |

## Permisos `product:*`

| Slug | Etiqueta (panel) |
|---|---|
| `product:update-client` | Editar cliente (producto) |
| `product:get-core-id` | Ver ID Core del cliente |
| `product:impersonate-client` | Entrar como usuario (redemption) |
| `product:consult-experian` | Consultar en Experian |
| `product:view-druo` | Ver cuenta Druo |
| `product:view-bank-docs` | Ver documentos bancarios |

## Matriz rol × permiso

| Permiso | sys_admin | core_admin | product_admin | core_read_only | product_read_only |
|---|:---:|:---:|:---:|:---:|:---:|
| Todos los `core:*` | ✅ | ✅ | ❌ | Parcial* | ❌ |
| Todos los `product:*` | ✅ | ❌ | ✅ | ❌ | Parcial** |

\* `core_read_only` solo incluye: `core:read-user-activity`, `core:get-client-history`, `core:simulate-payment-plan`, `core:get-calculator`, `core:download-calculator`, `core:download-payments-report`, `core:download-credits-report`.
\*\* `product_read_only` solo incluye `product:get-core-id`.

## Endpoints protegidos por permiso específico (verificado en `routes.ts`)

| Endpoint | Permiso requerido |
|---|---|
| `POST /product/clients/:id/impersonate` | `product:impersonate-client` |
| Consulta de ID Core del cliente | `product:get-core-id` |
| Consultas a Experian (2 endpoints) | `product:consult-experian` |
| Ver cuenta Druo (2 endpoints) | `product:view-druo` |
| Ver documentos bancarios (2 endpoints) | `product:view-bank-docs` |

## Endpoints protegidos por rol elevado (`requireAdmin`, no por permiso granular)

- `POST /auth/register`
- `GET /users`, `GET /users/:id`, `PATCH /users/:id/role`, `PATCH /users/:id/details`
- `POST /users/:id/reset-password`, `DELETE /users/:id`
- `GET /audit/actions`

## Endpoints exclusivos de `sys_admin` (`requireSysAdmin`)

- `GET /system/core-health`
- `GET /system/third-party-status`
- `GET /system/github-actions/runs`
- `GET /system/cloud-sql-status`
- `GET /system/stg-deploy/meta` (y endpoint adicional de despliegue)

> **Detalle técnico relevante:** `requireSysAdmin` valida el rol contra la **base de datos** (consulta `findById` en cada request), no contra el JWT emitido al iniciar sesión. Esto se documenta explícitamente en el código: evita que un usuario recién promovido a `sys_admin` reciba `403` hasta que vuelva a iniciar sesión, porque el chequeo siempre usa el rol vigente en BD.

## Excepción de desarrollo (`REQUIRE_AUTH=false`)

Todos los middlewares de autenticación (`authenticate`, `requireAdmin`, `requireSysAdmin`, `requirePermission`) respetan la variable de entorno `REQUIRE_AUTH`. Si es `'false'`, la autenticación se omite por completo y se inyecta un usuario simulado (`dev-user-id`, rol `sys_admin`), útil para entornos de desarrollo local. **Riesgo a vigilar:** debe confirmarse que esta variable nunca quede en `'false'` en ambientes de staging/producción.

## Referencias

`packages/kernel/src/common/admin-panel-permissions.ts`; `backends/admin/src/routes.ts`; `backends/admin/src/middleware/*.ts`.