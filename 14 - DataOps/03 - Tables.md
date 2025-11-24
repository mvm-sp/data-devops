
---

# Tabelas comparativas

---

## A) DataOps vs DevOps (visão rápida)

| Dimensão            |                                                    DataOps | DevOps                                            |
| ------------------- | ---------------------------------------------------------: | ------------------------------------------------- |
| Foco principal      | Datasets confiáveis, pipelines ETL/ELT, qualidade de dados | Aplicações, releases, infraestrutura de aplicação |
| Entregável          |           Tabelas/datasets versionados, catálogos, linagem | Artefatos de aplicação (builds, containers)       |
| Testes              |               Testes de dados (schema, qualidade, valores) | Unit/integration/e2e de software                  |
| Orquestração        |                 Orquestradores de dados (Airflow, Dagster) | Orquestração CI/CD (Jenkins, GitHub Actions)      |
| Observabilidade     |                  Freshness, latência, volume, data lineage | Latência de API, erro, CPU, logs                  |
| Governança          |          Catálogo, lineage, políticas de dados (LGPD/GDPR) | Controle de acesso, secrets, conformidade infra   |
| Ferramentas típicas |                dbt, Great Expectations, Airbyte, Snowflake | Kubernetes, Terraform, Docker, Prometheus         |

---

## B) Comparativo de ferramentas (foco DataOps)

| Camada             | Ferramenta                                  | Uso principal                      | Quando escolher                                                       |
| ------------------ | ------------------------------------------- | ---------------------------------- | --------------------------------------------------------------------- |
| Ingestão           | Airbyte / Fivetran                          | Conectores ELT prontos             | Quando quiser ingestão rápida com manutenção baixa                    |
| Streaming          | Kafka / PubSub / Kinesis                    | Ingestão em tempo real             | Latência baixa / alto throughput                                      |
| Orquestração       | Airflow / Dagster / Prefect                 | Agendamento & dependências         | Airflow para maturidade; Dagster/Prefect para testes e design modular |
| Transformação      | dbt / Spark / Databricks                    | Transformações SQL e pipelines ELT | dbt para SQL-first; Spark para processamento pesado                   |
| Armazenamento      | Snowflake / BigQuery / Redshift / S3 (lake) | Warehouse ou data lake             | Escolha por custo, escalabilidade e padrões                           |
| Observabilidade    | Monte Carlo / Soda / Great Expectations     | Data quality & lineage             | Quando precisar SLAs de qualidade e rastreabilidade                   |
| Catalog/Governança | DataHub / OpenMetadata / Collibra           | Catálogo de ativos e lineage       | Empresas com requisitos fortes de compliance                          |

---

## C) KPIs recomendados para DataOps (por categoria)

### Operacionais

| KPI                         | Descrição                        |                Meta sugerida |
| --------------------------- | -------------------------------- | ---------------------------: |
| Pipeline success rate       | % de runs sem falha              |                       >= 99% |
| Mean Time To Recover (MTTR) | Tempo médio para corrigir falhas | < 1 hora (dependendo do SLA) |
| Job duration                | Tempo médio de execução por job  |               Baseline + 20% |

### Qualidade de Dados

| KPI                               | Descrição                              |  Meta sugerida |
| --------------------------------- | -------------------------------------- | -------------: |
| Freshness                         | Tempo desde a última atualização       | < SLA (ex: 1h) |
| % de registros inválidos          | % de registros com falhas de validação |         < 0.1% |
| % de tabelas com testes aprovados | Percentual de tabelas com test-suite   |   100% em PROD |

### Adoção e Produto

| KPI                               | Descrição                                       |
| --------------------------------- | ----------------------------------------------- |
| Time to onboard dataset           | Tempo para disponibilizar novo dataset para uso |
| Número de consumidores            | Quantos squads consomem o dataset               |
| SLA de disponibilidade de dataset | Percentual de tempo em que dataset atende SLAs  |

---

# Integração e CI/CD sugeridos

* **Git**: versionar tudo — dbt models, scripts Airflow/Dagster, Terraform.
* **CI** (ex.: GitHub Actions):

  * Lint (SQLLint, flake8)
  * `dbt compile` + `dbt run --models +test` em PRs (com sandbox)
  * Testes unitários dos ops (Dagster) e scripts de ingest
  * Terraform fmt/validate + plan
* **CD**:

  * Deploy do DAG (Airflow) para ambiente de staging via pipeline automatizado
  * Promover via pipeline (merge protected) para prod
* **Observabilidade**:

  * Exportar métricas para Prometheus/Datadog
  * Logs centralizados (ELK/CloudWatch)
  * Alertas (Slack/PagerDuty) para MTTR baixos

---

# Checklist rápido para implantar os templates

1. Provisionar infra (Terraform): buckets S3, roles IAM, banco de metadados.
2. Configurar orquestrador: Airflow/Dagster (k8s / managed).
3. Implantar projeto dbt e profiles (com secrets em vault).
4. Integrar qualidade: Great Expectations / Soda com checkpoints.
5. Implementar CI: PR -> test dbt + lint + terraform plan.
6. Monitoramento e catálogo: instrumentar métricas e registrar datasets.

---

