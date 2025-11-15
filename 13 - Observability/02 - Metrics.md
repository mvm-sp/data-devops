
# Tabela de Métricas por Camada de Observabilidade em Engenharia de Dados

```markdown
| Camada                       | Métrica / Indicador                  | Descrição                                                                                   |
|-----------------------------|--------------------------------------|---------------------------------------------------------------------------------------------|
| **Infraestrutura**          | Uso de CPU                           | Percentual de processamento usado por clusters, VMs, nodes ou containers.                   |
|                             | Uso de Memória                       | Quantidade de memória consumida vs. disponível.                                             |
|                             | I/O de Disco                          | Taxa de leitura/gravação impactando performance de ETLs, DWs e jobs distribuídos.           |
|                             | Latência de Rede                     | Tempo de comunicação entre nós, serviços e sistemas distribuídos.                           |
|                             | Disponibilidade de Máquinas          | Uptime de clusters (Spark, EMR, Databricks, Kubernetes).                                    |
|                             | Autoscaling                          | Número de nós adicionados/removidos dinamicamente.                                          |
|                             | Uso de Storage                       | Crescimento de buckets, tabelas e armazenamento bruto.                                      |
|                             | Custo por Recurso                    | Gastos agregados por cluster, container, VM, job e serviços cloud.                          |
|                             | Limite de Throughput                | Limites atingidos em streaming, filas e tópicos.                                            |
|                             | Temperatura de Serviços              | Indicadores térmicos e throttling em serviços gerenciados.                                  |
|-----------------------------|--------------------------------------|---------------------------------------------------------------------------------------------|
| **Aplicação / Pipeline**    | Latência de Pipeline                 | Tempo de execução total de cada DAG/job.                                                    |
|                             | Latência por Etapa                   | Tempo de execução por tarefa (task run).                                                    |
|                             | Taxa de Falhas                       | Percentual de jobs ou etapas que falharam.                                                  |
|                             | Retries                              | Quantidade de tentativas automáticas após erro.                                             |
|                             | Backpressure                         | Indicador de sobrecarga em pipelines de streaming.                                          |
|                             | Throughput de Processamento          | Registros/segundo processados por job, microbatch ou tópico.                                |
|                             | Backlog de Mensagens                 | Mensagens acumuladas em filas como Kafka ou Kinesis.                                        |
|                             | SLA de Execução                      | Comparação entre tempos reais e esperados do pipeline.                                      |
|                             | Integridade de Conexões              | Erros de conexão com bancos, APIs, DWs, sistemas externos.                                  |
|                             | Utilização de Workers                | Quantidade de workers ocupados vs. livres (Airflow, Dagster, Kubernetes).                   |
|-----------------------------|--------------------------------------|---------------------------------------------------------------------------------------------|
| **Dados**                   | Freshness (Atualidade)              | Tempo desde a última atualização dos dados.                                                 |
|                             | Volume de Dados                      | Quantidade de linhas/arquivos ingeridos por hora/dia.                                       |
|                             | Data Drift                           | Mudança nas distribuições estatísticas ao longo do tempo.                                   |
|                             | Schema Drift                         | Mudanças inesperadas em colunas, tipos ou estrutura.                                        |
|                             | Taxa de Nulos/Valores Inválidos      | Percentual de campos faltantes ou inconsistentes.                                           |
|                             | Distribuição Estatística             | Média, variância, percentis, entropia, frequências.                                         |
|                             | Duplicidade                          | Quantidade de registros duplicados ou inconsistentes.                                       |
|                             | Consistência entre Tabelas           | Divergências entre tabelas upstream e downstream.                                           |
|                             | Qualidade de Dados (DQ Score)        | Métrica agregada baseada em regras de qualidade.                                            |
|                             | Linhagem dos Dados                   | Dependências entre tabelas e impacto de alterações.                                         |
|-----------------------------|--------------------------------------|---------------------------------------------------------------------------------------------|
| **Negócios**                | SLA/SLO de Dados                     | Atendimento a prazos, qualidade e disponibilidade acordados.                                |
|                             | KPIs de Domínio                      | Indicadores específicos (pedidos, clientes, eventos, faturamento).                          |
|                             | Consumo de Dados                     | Quem usa, com que frequência, e quais datasets são mais críticos.                           |
|                             | Custos Operacionais por Pipeline     | Custo estimado por execução diária/mensal.                                                  |
|                             | ROI do Pipeline                      | Retorno financeiro/operacional gerado por fluxo de dados.                                   |
|                             | Indicadores de Risco                 | Probabilidade de falha, impacto em áreas críticas do negócio.                               |
|                             | Confiabilidade do Dado               | Percepção das áreas usuárias sobre a confiabilidade dos datasets.                           |
|                             | Aderência a Governança               | Cumprimento de políticas de auditoria, privacidade e compliance.                            |
|                             | Disponibilidade de Dados             | Tempo em que os dados ficaram acessíveis para uso.                                          |
|                             | Tempo de Resposta a Incidentes      | Velocidade na investigação e resolução de incidentes relacionados a dados.                  |
```

---

