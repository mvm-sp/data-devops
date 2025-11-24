
# Templates de Pipeline DataOps

---

## 1) Airflow — DAG de exemplo (Python)

Use para orquestrar ingestão → transformação dbt → qualidade → deploy/registro.

```python
# dags/dataops_pipeline.py
from datetime import datetime, timedelta
from airflow import DAG
from airflow.operators.bash import BashOperator
from airflow.operators.python import PythonOperator
from airflow.sensors.external_task import ExternalTaskSensor

# Configs básicas
default_args = {
    "owner": "data-team",
    "depends_on_past": False,
    "retries": 1,
    "retry_delay": timedelta(minutes=5),
    "email_on_failure": True,
    "email": ["dataops-alerts@example.com"],
}

with DAG(
    dag_id="dataops_ingest_transform_validate",
    default_args=default_args,
    description="Ingest -> dbt transform -> quality checks -> publish",
    schedule_interval="0 */4 * * *",  # a cada 4 horas
    start_date=datetime(2025, 1, 1),
    catchup=False,
    max_active_runs=1,
) as dag:

    # 1. Ingest (ex: chamada a um job que coloca arquivos no S3)
    ingest = BashOperator(
        task_id="ingest_from_api",
        bash_command="""
        /usr/local/bin/python /opt/airflow/dags/scripts/ingest_api_to_landing.py --output s3://my-bucket/landing/{{ ds }}
        """,
    )

    # 2. Wait for files (opcional: sensor customizado)
    wait_for_files = BashOperator(
        task_id="wait_for_ingest_marker",
        bash_command="""
        # exemplo simples; em produção, use S3KeySensor/ExternalTaskSensor
        python /opt/airflow/dags/scripts/wait_for_s3_key.py --bucket my-bucket --prefix landing/{{ ds }}
        """,
    )

    # 3. Trigger dbt run (ex: dbt-core em container ou ambiente virtual)
    run_dbt = BashOperator(
        task_id="dbt_run",
        bash_command="""
        cd /opt/dbt_project &&
        dbt deps &&
        dbt seed --profiles-dir . --profiles-dir ./profiles &&
        dbt run --profiles-dir . --target prod &&
        dbt test --profiles-dir . --target prod
        """,
    )

    # 4. Data quality checks adicionais (ex: Great Expectations)
    run_ge = BashOperator(
        task_id="great_expectations_validation",
        bash_command="""
        cd /opt/great_expectations &&
        great_expectations checkpoint run my_checkpoint
        """,
    )

    # 5. Publish / register (ex: atualizar catálogo, registrar linha de dados)
    publish = BashOperator(
        task_id="register_dataset_catalog",
        bash_command="""
        python /opt/airflow/dags/scripts/register_catalog.py --dataset transformed/my_table --env prod
        """,
    )

    # 6. Notificação
    notify = BashOperator(
        task_id="notify_team",
        bash_command='curl -X POST -H "Content-type: application/json" --data \'{"text":"Pipeline concluído: {{ dag.dag_id }} {{ ts }}"}\' $SLACK_WEBHOOK',
    )

    # Orquestração
    ingest >> wait_for_files >> run_dbt >> run_ge >> publish >> notify
```

**Notas**

* Prefira usar `S3KeySensor`, `S3PrefixSensor`, ou operadores específicos do provedor (GoogleCloudStorageObjectSensor).
* Use conexões Airflow (Airflow Connections) para credenciais (S3, Snowflake, BigQuery).
* Integre com observabilidade: envie métricas (SLA, duração) para Prometheus/StatsD.

---

## 2) Dagster — Job/Graph exemplo (Python)

Dagster trata ops/graphs como objetos, bom para testes unitários e type-safe.

```python
# jobs/dataops_job.py
from dagster import op, job, op, get_dagster_logger, resource
from dagster import GraphOut, DynamicOut, DynamicOutput

@op
def ingest_api(context) -> str:
    context.log.info("Iniciando ingestão")
    # lógica: salvar em staging (ex: S3) e retornar path
    path = "s3://my-bucket/landing/2025-11-22/"
    return path

@op
def run_dbt(context, staging_path: str) -> dict:
    context.log.info(f"Executando dbt com staging: {staging_path}")
    # chame subprocess dbt ou use dbt-core como biblioteca
    # retornar info de execução (ex: rows_processed)
    return {"status": "success", "rows": 12345}

@op
def data_quality(context, dbt_result: dict) -> bool:
    context.log.info("Rodando checagens de qualidade")
    # chamar Great Expectations ou validações custom
    return True

@op
def publish_catalog(context, ok: bool):
    context.log.info("Registrando dataset no catálogo")
    # chamada a API do catálogo (DataHub, OpenMetadata)
    return {"catalog_id": "dataset_abc"}

@job
def dataops_job():
    staging = ingest_api()
    dbt_res = run_dbt(staging)
    ok = data_quality(dbt_res)
    publish_catalog(ok)
```

**Recomendações**

* Use resources para credenciais/clients (S3, dbt) e para teste local.
* Combine com schedules e sensors do Dagster para triggers baseados em eventos.
* Teste cada `op` isoladamente com fixtures.

---

## 3) dbt — Estrutura mínima + exemplo de model e testes

Um projeto `dbt` (data build tool) é a estrutura organizada que contém todo o código, configurações e artefatos necessários para criar, transformar, testar, documentar e versionar pipelines de dados usando SQL como código.

Ele é a base do trabalho com dbt: tudo o que o dbt faz — compilar SQL, executar transformações, criar tabelas/views, rodar testes, gerar documentação — acontece dentro de um projeto dbt.

Estrutura básica:

```
dbt_project.yml
profiles.yml
models/
  staging/
    stg_orders.sql
  marts/
    m_orders.sql
tests/
macros/
```

`dbt_project.yml` (essencial):

```yaml
name: 'my_dbt_project'
version: '1.0.0'
config-version: 2

profile: 'prod_profile'

model-paths: ["models"]
seed-paths: ["seeds"]
target-path: "target"
analysis-paths: ["analysis"]
test-paths: ["tests"]
```

`models/staging/stg_orders.sql`

```sql
{{ config(materialized='view') }}

with raw as (
  select
    id,
    created_at,
    amount,
    customer_id,
    status
  from {{ source('landing', 'orders') }}
)

select
  id,
  cast(created_at as timestamp) as created_at,
  cast(amount as numeric) as amount,
  customer_id,
  lower(status) as status
from raw
```

`models/marts/m_orders.sql`

```sql
{{ config(materialized='table') }}

with orders as (
  select * from {{ ref('stg_orders') }}
)

select
  customer_id,
  count(*) as total_orders,
  sum(amount) as total_amount,
  min(created_at) as first_order,
  max(created_at) as last_order
from orders
group by customer_id
```

`models/schema.yml` (tests)

```yaml
version: 2

sources:
  - name: landing
    tables:
      - name: orders

models:
  - name: stg_orders
    description: "Staging orders"
    columns:
      - name: id
        tests:
          - unique
          - not_null
      - name: amount
        tests:
          - not_null
          - accepted_values:
              values: [0, 1, 2, 3]  # exemplo

  - name: m_orders
    description: "Marts orders agregadas"
    columns:
      - name: total_orders
        tests:
          - not_null
```

**Boas práticas**

* Versione `models/`, `macros/` e `profiles.yml` separadamente (procure não commitar credenciais).
* Integre `dbt test` no pipeline CI.
* Use `dbt snapshot` para slowly changing dimensions quando necessário.

---

## 4) Terraform — Módulo mínimo para S3 + IAM (ex.: Data Lake landing + role)

Estrutura:

```
terraform/
  main.tf
  variables.tf
  outputs.tf
  modules/
    s3_bucket/
      main.tf
      variables.tf
      outputs.tf
```

`modules/s3_bucket/main.tf`

```hcl
resource "aws_s3_bucket" "this" {
  bucket = var.bucket_name
  acl    = var.acl

  lifecycle_rule {
    id      = "archive-older-30"
    enabled = true

    transition {
      days          = 30
      storage_class = "GLACIER"
    }

    expiration {
      days = 365
    }
  }

  server_side_encryption_configuration {
    rule {
      apply_server_side_encryption_by_default {
        sse_algorithm = "AES256"
      }
    }
  }

  tags = var.tags
}
```

`modules/s3_bucket/variables.tf`

```hcl
variable "bucket_name" { type = string }
variable "acl" { type = string, default = "private" }
variable "tags" { type = map(string), default = {} }
```

`main.tf` (root)

```hcl
provider "aws" {
  region = var.region
}

module "landing_bucket" {
  source = "./modules/s3_bucket"
  bucket_name = var.landing_bucket_name
  tags = {
    "Project" = "dataops"
    "Env"     = var.environment
  }
}

resource "aws_iam_role" "data_pipeline_role" {
  name = "data-pipeline-role-${var.environment}"
  assume_role_policy = data.aws_iam_policy_document.assume_role.json
}

data "aws_iam_policy_document" "assume_role" {
  statement {
    effect = "Allow"
    principals {
      type = "Service"
      identifiers = ["glue.amazonaws.com", "ec2.amazonaws.com"] # ex.
    }
    actions = ["sts:AssumeRole"]
  }
}
```

`variables.tf` (root)

```hcl
variable "region" { default = "us-east-1" }
variable "environment" { default = "prod" }
variable "landing_bucket_name" { default = "my-dataops-landing-prod" }
```

**Recomendações**

* Separe ambientes (dev/staging/prod) por workspaces ou pastas.
* Use state remota (S3 + DynamoDB lock) para colaboração.
* Mantendo infra como código: crie módulos para Glue/Catalog, IAM policy para acesso mínimo (least-privilege).
