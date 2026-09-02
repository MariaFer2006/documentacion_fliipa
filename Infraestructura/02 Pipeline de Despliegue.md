# Pipeline de despliegue (CI/CD)

El monorepo soporta dos vías de despliegue equivalentes por entorno: **CLI** (scripts bash, ejecutables desde el laptop del operador) y **GitHub Actions** (workflows por servicio o por flota). Ambas terminan aplicando la misma matriz de configuración (`config/deploy/*-service-matrix.json`).

## PROD

| Vía | Comando / disparo |
|---|---|
| CLI | `bash scripts/pdeploy-prod.sh --all` (toda la flota, en el orden de `deployOrder`) |
| CLI (subset) | `bash scripts/pdeploy-prod.sh webhooks b2b` |
| CLI (paquete nuevo) | `bash scripts/pdeploy-prod.sh --package apps/nuevo` (scaffold + deploy) |
| CLI (forzar rebuild) | `bash scripts/pdeploy-prod.sh checkout --force` |
| GitHub Actions | Actions → `PROD - creds-{slug}` → requiere input `confirm=DEPLOY` |

`pdeploy-prod.sh` es idempotente: valida o crea el Dockerfile del servicio, su entrada en la matriz, el workflow de GitHub y los *mounts* de secretos si faltan, antes de desplegar. Cada workflow `.github/workflows/creds-*-prod.yml` reproduce el mismo comportamiento vía Actions, por lo que ambas vías son intercambiables.

Los Dockerfiles nuevos parten de plantillas versionadas en [`docs/infra/templates/`](../README.md): `Dockerfile.node-service` (servicios Node) y `Dockerfile.next-app` (apps Next.js).

## STG / demo (`product-fintech-dev`)

La vía preferida es **GitHub Actions en paralelo** (matrix, una fila por servicio):

```bash
gh workflow run stg-deploy.yml -f slugs=all
gh workflow run stg-deploy.yml -f slugs=b2b,admin-back -f force=true
gh workflow run stg-deploy.yml -f slugs=b2b -f run_migrate=true

gh run list --workflow=stg-deploy.yml --limit 5
gh run watch
```

También se dispara automáticamente en cada push a `main` que toque `apps/`, `backends/`, `services/` o `packages/` (mapeo *path → slug* vía `scripts/lib/stg_detect_slugs.py`; los paquetes compartidos como `packages/kernel` o el lockfile disparan el redeploy de toda la flota).

El workflow asume la flota STG **ya provisionada** (Artifact Registry, Cloud SQL, service accounts, secretos montados): no ejecuta `--with-infra` ni siembra secretos. Las migraciones solo corren si el *path* modificado toca paquetes con base de datos, o si se pasa `-f run_migrate=true`.

La vía **laptop** (`scripts/deploy-dev.sh`, alias `pnpm deploy:dev`) queda para el primer aprovisionamiento de infraestructura, siembra de secretos/seeds, o como *fallback*:

```bash
pnpm deploy:dev                       # interactivo (pregunta infra / migraciones / build)
bash scripts/deploy-dev.sh --dry-run
bash scripts/deploy-dev.sh --skip-infra
pnpm deploy:dev -- admin-back         # un servicio, rebuild solo si cambió (fingerprint)
pnpm deploy:dev -- core admin-back --force
pnpm deploy:dev -- --with-infra --with-migrate --with-build --run-seeds
```

`deploy-dev.sh` corre en una *subshell* para que las variables `CREDITS_*` / `CLOUDSDK_*` no se filtren a la shell del operador. Existe además un asistente en el **panel admin** (`System → STG Deploy`, solo rol `sysadmin`) que arma el comando `gh workflow run …` o `pnpm deploy:dev -- …` recomendado, pero **no ejecuta** el despliegue por sí mismo; opcionalmente notifica el despliegue por Slack.

## Aislamiento PROD / STG en el pipeline

| | PROD | STG / DEV |
|---|---|---|
| Wrapper de contexto | `pdeploy-prod.sh` → `pin_prod_deploy_context` (fuerza `CREDITS_DEPLOY_ENV=prod`) | `deploy-dev.sh` / workflow `stg-deploy.yml` → `pin_dev_deploy_context` |
| Verificación | Los scripts comprueban `matrix.projectId == PROJECT_ID` y abortan si no coincide con el entorno activo | ídem |

Esta verificación evita, por ejemplo, que un despliegue de STG apunte por error a Cloud SQL o Secret Manager de PROD.

## Sincronización de URLs entre servicios

Después de cada despliegue que afecte endpoints consumidos por otros servicios:

```bash
bash scripts/prod-urls.sh              # sync → apply → verify
bash scripts/prod-urls.sh verify
```

El registro de URLs vive como secreto en Secret Manager (`creds-prod-url-registry` en PROD, `creds-dev-url-registry` en STG) y se calcula con `scripts/lib/prod_urls.py`, cruzando `url-bindings.json` con las URLs reales de Cloud Run (o con los orígenes públicos de `domains.prod.env` cuando `DEPLOY_PHASE=F`, ver [Dominio y Load Balancer](05 Dominio y Load Balancer.md)).

## Checklist para un servicio nuevo

1. Código en `apps/`, `backends/`, `gateways/` o `services/`.
2. `bash scripts/pdeploy-prod.sh --package <dir>` (genera Dockerfile, entrada en la matriz, workflow y mounts si faltan, y despliega).
3. Completar `url-bindings.json` si el servicio consume URLs de otros.
4. `bash scripts/prod-urls.sh`.
5. Commitear el Dockerfile, la entrada en la matriz y el workflow generados.

## Rollback

1. Cloud Run → seleccionar la revisión anterior → mover el 100% del tráfico, **o**
2. Re-ejecutar el workflow correspondiente con `git_ref` apuntando al SHA conocido como bueno.
