# Jobs batch y migraciones de base de datos

## Jobs batch (`jobs/`)

El paquete `@credits-platform/jobs` empaqueta tareas batch que corren como **Cloud Run Job** `creds-jobs-prod`, invocado con una variable `JOB_NAME` distinta por ejecución. Cada corrida pasa por `runWithAlerts`, que emite una `OperationalAlert` (inicio / fin / error) vía `@credits-platform/kernel` hacia Slack.

Estructura del paquete:

```text
jobs/
  src/
    cli.ts                 punto de entrada (lee JOB_NAME)
    handlers/
      index.ts              registro de jobs disponibles
      example-ping.ts        job de referencia
    lib/
      run-context.ts, run-with-alerts.ts, db.ts, logger.ts
```

A la fecha de esta revisión, el único job registrado en `handlers/index.ts` es `example-ping` (job de referencia/health-check del mecanismo de jobs), pensado como plantilla para futuros jobs reales.

Añadir un job nuevo:

1. Crear `src/handlers/<nombre>.ts` exportando un `JobDefinition`.
2. Registrarlo en `src/handlers/index.ts`.
3. Agregar una entrada de Cloud Scheduler apuntando al Job `creds-jobs-prod` con `JOB_NAME=<nombre>` (ver `scripts/provision-prod-jobs-schedulers.sh`).

Ejecución local:

```bash
cd jobs
pnpm exec tsx --env-file=.env src/cli.ts --job=example-ping
# o
JOB_NAME=example-ping pnpm start
```

Requiere `DB_HOST`, `DB_PORT`, `DB_USER`, `DB_PASSWORD` y opcionalmente `CORE_DB_NAME` (default `fliipa_banking_core`). Para probar alertas de Slack en local: `SLACK_MODE=online` + `SLACK_WEBHOOK_URL=…` (si no, quedan en modo *mock*/consola).

### Aprovisionamiento y ejecución en PROD

```bash
bash scripts/provision-prod-jobs.sh              # build/push/upsert del Job (+ Cloud SQL + secreto Slack)
bash scripts/provision-prod-jobs-schedulers.sh   # Cloud Scheduler, hasta 2×/día por job
# o vía GitHub: Actions → PROD - creds-jobs CI/CD → confirm=DEPLOY

gcloud run jobs execute creds-jobs-prod \
  --region=us-central1 --project=product-fintech --wait \
  --update-env-vars=JOB_NAME=example-ping
```

`scripts/provision-prod-jobs-schedulers.sh` define, verificado en el propio script, un arreglo `JOB_SCHEDULES` con el formato `nombre-scheduler|JOB_NAME|cron`. A la fecha de esta revisión contiene únicamente dos entradas por defecto para el job de referencia:

| Scheduler | `JOB_NAME` | Cron (`America/Bogota`) |
|---|---|---|
| `creds-jobs-example-ping-am` | `example-ping` | `0 0 * * *` (00:00) |
| `creds-jobs-example-ping-pm` | `example-ping` | `0 12 * * *` (12:00) |

Cada Cloud Scheduler invoca `creds-jobs-prod` vía la Run Jobs API con un *override* de `JOB_NAME`, usando como identidad la service account `creds-runtime-product@<PROJECT_ID>.iam.gserviceaccount.com`. Nuevos jobs reales deben añadir su propia fila a `JOB_SCHEDULES` (o su propio scheduler) antes de considerarse operativos en producción.

Bases de datos lógicas accesibles desde jobs (por variable de entorno): `CORE_DB_NAME` (default `fliipa_banking_core`), `B2B_DB_NAME`, `RULES_ENGINE_DB_NAME`, etc. El secreto de Slack de operaciones (`creds-slack-webhook-url` → `SLACK_WEBHOOK_URL`) también se monta en `b2b`.

## Migraciones de base de datos

Las migraciones (TypeORM) corren como su propio **Cloud Run Job**, `creds-migrate-prod`, construido con una imagen dedicada (`infra/migrate/Dockerfile`) que compila únicamente los paquetes con acceso a base de datos (`kernel`, `b2b-gateway`, `communications`, `rules-engine`) y ejecuta `scripts/migrate-prod-packages.sh` como *entrypoint*.

```bash
bash scripts/run-prod-migrations.sh    # levanta el Cloud SQL Auth Proxy y corre las migraciones
bash scripts/run-prod-seeds.sh         # seeds paramétricos (usuario admin + settings)
```

En STG, el workflow `stg-deploy.yml` solo dispara migraciones cuando el *path* modificado toca un paquete con base de datos, o cuando se invoca con `-f run_migrate=true`; localmente, `scripts/run-dev-seeds.sh` corre seeds contra el proxy SQL de STG (puerto `9877`).
