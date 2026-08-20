# 1. Roles del panel administrativo

[← Volver al índice](README.md)

El panel administrativo (backend `admin`, conocido internamente como *Frankor*) define 5 roles de aplicación (`AppRole` / `UserRole`), almacenados como texto libre (`varchar`) en la columna `role` de la tabla `users`, con un arreglo `extra_permissions` (jsonb) para otorgar permisos puntuales adicionales fuera del rol base.

| Rol (código) | Etiqueta | Alcance |
|---|---|---|
| `sys_admin` | Sys Admin | Todos los permisos de `core` + todos los de `product`. Único rol habilitado para las rutas de `/system/*` (salud del core, base de datos, terceros, despliegues) y para gestión de usuarios (`/users/*`). |
| `core_admin` | Core Admin | Todos los permisos de `core` (gestión de usuarios finales, cupo, desembolsos, pagos, configuración, reportes). Sin permisos de `product`. |
| `product_admin` | Product Admin | Todos los permisos de `product` (impersonar clientes, consultar Experian, ver Druo, ver documentos bancarios). Sin permisos de `core`. |
| `core_read_only` | Core Reader | Subconjunto de solo lectura de `core`: actividad de usuario, historial de cliente, simulación de plan de pagos, uso/descarga de calculadora, descarga de reportes de créditos y pagos. **Rol por defecto** de un usuario nuevo (`default: 'core_read_only'` en el modelo `User` y en `buildEffectivePermissionSlugs` cuando el rol no es reconocido). |
| `product_read_only` | Product Reader | Solo el permiso `product:get-core-id` (ver ID Core del cliente). |

## Roles "elevados" del panel (`ELEVATED_PANEL_ROLES`)

Además del sistema de permisos granular, existe una verificación de rol elevado (`isElevatedPanelRole`) usada por el middleware genérico `requireAdmin`, para rutas de administración del panel que no están cubiertas por un permiso específico (por ejemplo, gestión de usuarios y auditoría):

- `sys_admin`
- `core_admin`
- `product_admin`

`core_read_only` y `product_read_only` **no** son roles elevados: no pueden gestionar usuarios ni ver la actividad de otros usuarios (solo la propia).

## Usuario administrador de arranque (seed)

El sistema crea/realinea de forma idempotente un usuario administrador base en cada ejecución de seeds:

| Campo | Valor |
|---|---|
| Correo | `admin@sumz.co` |
| Nombre | Frankor Admin |
| Rol | `sys_admin` |
| Permisos extra | Ninguno (`[]`) |

> El seed **realinea** email, nombre, contraseña y `extra_permissions` a estos valores canónicos si el usuario ya existe pero difiere — es decir, no es un simple "crear si no existe", sino una fuente de verdad idempotente para este usuario específico.

## Evolución del modelo (histórico verificado en migraciones)

1. **Modelo original:** `role` como enum con solo dos valores (`user` / `admin`).
2. **Migración `UsersAppRoleExtraPermissions`:** se agrega `app_role` (varchar, rol de panel) y `extra_permissions` (jsonb), migrando `admin` → `sys_admin` y `user` → `core_read_only`.
3. **Migración `UsersRoleVarcharDropEnum`:** se elimina la columna `role` (enum) y el tipo `users_role_enum`; `app_role` se renombra a `role` como `varchar(32)`, quedando el modelo actual de 5 roles de panel. Esta migración **no soporta rollback** (`down()` lanza error explícito: "recrear enum user/admin es lossy").

## Referencias

`packages/kernel/src/common/admin-panel-permissions.ts`; `packages/kernel/src/db/models/User.ts`; `packages/kernel/src/db/migrations/1780100000000-UsersAppRoleExtraPermissions.ts`; `packages/kernel/src/db/migrations/1780200000000-UsersRoleVarcharDropEnum.ts`; `packages/kernel/src/db/seeds/admin-user.seed.ts`; `backends/admin/src/auth-roles.ts`.