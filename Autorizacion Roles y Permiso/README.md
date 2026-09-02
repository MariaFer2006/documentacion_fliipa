# Autorizaciones, Roles y Permisos

Sección técnica que documenta el modelo de autenticación, roles y permisos implementado en `credits-platform-main`, verificado directamente contra el código fuente.

## Contenido

1. [Roles del panel administrativo](01 roles del panel administrativo.md)
2. [Matriz de permisos por acción](02 matriz de permisos.md)
3. [Autenticación de clientes (checkout / redemption)](03 autenticacion de clientes.md)
4. [Impersonación de clientes (entrar como usuario)](04 impersonacion de clientes.md)
5. [Pendientes y riesgos identificados](05 pendientes y riesgos.md)

## Alcance

Esta sección cubre exclusivamente el **backend `admin`** (panel administrativo, roles `sys_admin` / `core_admin` / `product_admin` / `core_read_only` / `product_read_only`) y la **autenticación de clientes empresariales** en `b2b` / `redemption` / `checkout` (documento + PIN, sin roles). No cubre autorización a nivel de infraestructura (IAM de GCP, secretos, etc.), que está fuera del alcance de este repositorio funcional.

## Fuentes consultadas

- `packages/kernel/src/common/admin-panel-permissions.ts` (fuente única de roles y permisos, compartida por `kernel`, `backends/admin` y el SDK del panel).
- `backends/admin/src/middleware/auth.middleware.ts`, `sys-admin.middleware.ts`, `require-permission.middleware.ts`.
- `backends/admin/src/auth-roles.ts`, `backends/admin/src/permissions.ts`.
- `backends/admin/src/routes.ts` (aplicación real de los middlewares por endpoint).
- `packages/kernel/src/db/models/User.ts` y migraciones `1780100000000-UsersAppRoleExtraPermissions.ts`, `1780200000000-UsersRoleVarcharDropEnum.ts`.
- `packages/kernel/src/db/seeds/admin-user.seed.ts`.
- `backends/b2b/src/services/login.ts`, `backends/b2b/src/services/impersonate.service.ts`, `backends/b2b/src/controllers/auth/impersonate.ts`.
- `backends/admin/src/controllers/product-impersonate.controller.ts`.

> **Nota de versión:** esta sección se crea el 20/08/2026 a partir de la revisión del código fuente de `credits-platform-main`. No existía previamente ninguna carpeta o sección dedicada a autorizaciones, roles y permisos en `documentacion_fliipa`; los actores de negocio (Analista de riesgo, Administrador, etc.) ya estaban descritos en [Negocio/Actores](../Negocio/Actores/README.md), pero sin el detalle técnico de roles/permisos a nivel de sistema.