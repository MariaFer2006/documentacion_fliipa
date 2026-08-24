# Dominio y Load Balancer

## Estado actual

La plataforma opera hoy en **Fase 1**: todos los servicios públicos se sirven directamente en sus URLs `*.run.app` de Cloud Run. **No existen** Cloud DNS ni un HTTPS Load Balancer en `product-fintech`. El objetivo (Fase F) es servir `fliipa.com` y `api.fliipa.com` delante de los Cloud Run públicos.

DNS histórico: el apex y `www` apuntaban a Webflow; `api.fliipa.com` no existía.

## Prerrequisitos fuera de GCP

| # | Qué | Cómo validar |
|---|---|---|
| 1 | Acceso al panel de `fliipa.com` (Network Solutions y/o Webflow) | Login funcional |
| 2 | Decisión sobre el *cutover* de Webflow | ¿Se reemplaza el sitio actual o se redirige a `/checkout`? |
| 3 | Renovación del dominio | Verificar WHOIS / alerta ~2026-09-25 |

## Enrutamiento objetivo (Load Balancer → Cloud Run)

Dos hosts, con *paths* que coinciden con el `basePath` ya configurado en las apps Next.js y con las APIs ya usadas en Fase 1:

| Host | Path | Backend Cloud Run |
|---|---|---|
| `fliipa.com` | `/checkout`, `/checkout/*` | `creds-checkout-prod` |
| `fliipa.com` | `/redemption`, `/redemption/*` | `creds-redemption-prod` |
| `fliipa.com` | `/admin`, `/admin/*` | `creds-admin-prod` |
| `fliipa.com` | `/` (opcional) | redirección a `/checkout` |
| `api.fliipa.com` | `/api/v1/*` (b2b) | `creds-b2b-prod` |
| `api.fliipa.com` | `/admin/api/v1/*` o path de admin-back | `creds-admin-back-prod` |
| `api.fliipa.com` | `/api/v1/webhooks/*` | `creds-webhooks-prod` |

Los servicios internos (`core`, etc.) **no** se exponen en el Load Balancer: siguen siendo IAM-only / accesibles solo por `*.run.app` interno.

## Checklist de aprovisionamiento en GCP (orden sugerido)

1. IP estática global + HTTPS Load Balancer (URL map según la tabla anterior) + *serverless NEGs* hacia cada Cloud Run público.
2. Certificado *managed* para `fliipa.com`, `www` (si aplica) y `api.fliipa.com` — queda en estado `PROVISIONING` hasta que el DNS apunte al Load Balancer.
3. DNS (Cloud DNS o registros en el registrador actual): `A`/`AAAA` del apex → IP del LB; `CNAME`/`A` de `api` → LB.
4. Esperar a que el certificado quede `ACTIVE`.
5. *Cutover* en el registrador (si se usa Cloud DNS, delegar los NS a Google).
6. En el repositorio, activar los orígenes públicos en `config/deploy/domains.prod.env`:

```bash
DEPLOY_PHASE=F
PUBLIC_WEB_ORIGIN=https://fliipa.com
PUBLIC_API_ORIGIN=https://api.fliipa.com
```

7. Propagar las URLs y reconstruir los frontends (las variables `NEXT_PUBLIC_*` se inyectan en *build-time*):

```bash
bash scripts/prod-urls.sh
bash scripts/pdeploy-prod.sh checkout redemption admin --force
# o vía Actions: PROD - creds-checkout | creds-redemption | creds-admin
```

8. *Smoke test*: `https://fliipa.com/checkout`, login de admin, endpoints de salud en `api.fliipa.com`.
9. Opcional: re-registrar webhooks de terceros (Druo, Zenvia) con la URL final bajo `api.fliipa.com`.

## Código/config que ya anticipa la Fase F

| Pieza | Rol |
|---|---|
| `config/deploy/domains.prod.env` | Único *switch* de orígenes públicos |
| `scripts/lib/prod_urls.py` (`build_computed`) | Si `DEPLOY_PHASE=F` y hay orígenes configurados, calcula las URLs públicas finales |
| `config/deploy/url-bindings.json` | Define qué servicio consume cada URL `computed.*` / `services.*` |
| `basePath` de Next.js | Ya alineado a `/checkout`, `/redemption`, `/admin`, los mismos paths del LB objetivo |

No hace falta rediseñar los *bindings*: al pasar `DEPLOY_PHASE` a `F`, correr `prod-urls.sh` y reconstruir los frontends Next.js, las variables de CORS, `NEXT_PUBLIC_*` y `APP_BASE_URL` deberían apuntar automáticamente al dominio final.

## Preguntas abiertas (bloquean el *cutover*)

- ¿Quién tiene la custodia del panel de DNS de `fliipa.com`?
- ¿Estrategia definitiva frente a Webflow (reemplazo total o redirección)?
- ¿Path exacto de `admin-back` y `webhooks` bajo `api.fliipa.com`?
- ¿`www` debe redirigir al apex o servirse igual que este?
