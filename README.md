# Pipeline de Dados no Databricks — Medalhão (Automobile)

Este repositório organiza um pipeline ELT no Databricks baseado em notebooks ordenados, seguindo a arquitetura Medalhão (Landing -> Bronze -> Silver -> Gold) para o domínio de automóveis.

## Visão Geral
- Fluxo principal: `001 -> 002 -> 003 -> 004` e limpeza com `005`.
- Cada notebook é focado em uma camada do medalhão e é idealmente idempotente.
- A execução pode ser orquestrada por um Job do Databricks com tarefas encadeadas.

## Arquitetura (Medalhão)
- **Fonte de Dados**: Banco PostgreSQL em nuvem (Supabase) - ingestão direta via JDBC
- **Bronze**: Ingestão fiel dos dados do banco em nuvem, com mínimo tratamento (auditabilidade).
- **Silver**: Limpeza, padronização, enriquecimento e modelagem para consumo analítico.
- **Gold**: Métricas, agregações e curadorias otimizadas para consumo de negócio.

```mermaid
flowchart LR
    DB[(Banco PostgreSQL<br/>Supabase)] --> B[Bronze]
    B --> S[Silver]
    S --> G[Gold]
```

## Estrutura do Projeto
```
notebooks/
  001_-environment-preparation.ipynb      # Preparação de ambiente e assets
  002_-landing_to_bronze_automobile.ipynb # Ingestão Banco -> Bronze (automobile)
  003_-bronze_to_silver_automobile.ipynb  # Transformação Bronze -> Silver (automobile)
  004_-silver_to_gold_automobile.ipynb    # Curadoria/Agrupações Silver -> Gold (automobile)
  005_-destroying-environment.ipynb       # Teardown/Limpeza de assets
```
## Estrutura do MKDocs
```
docs/
  arquitetura.md   # Arquitetura utilizada no projeto
  bronze.md        # Descrições da camada bronze
  silver.md        # Descrições da camada silver
  gold.md          # Descrições da camada gold
  index.md         # Página de início
  pipeline.md      # Pipeline dos dados
  fluxo.md         # Exemplificação dos fluxos entre as camadas
```


## Orquestração com Job do Databricks

| Ordem | Tarefa | Notebook |
|------:|--------|----------|
| 1 | environment_preparation | `notebooks/001_-environment-preparation.ipynb` |
| 2 | database_to_bronze | `notebooks/002_-landing_to_bronze_automobile.ipynb` |
| 3 | bronze_to_silver | `notebooks/003_-bronze_to_silver_automobile.ipynb` |
| 4 | silver_to_gold | `notebooks/004_-silver_to_gold_automobile.ipynb` |
| 5 | destroying_environment | `notebooks/005_-destroying-environment.ipynb` |

## Fonte de Dados

O pipeline consome dados diretamente de um **banco PostgreSQL hospedado no Supabase** (nuvem), utilizando conexão JDBC para ingestão em tempo real. Esta abordagem oferece:

- **Conectividade direta**: Elimina a necessidade de arquivos intermediários
- **Dados atualizados**: Acesso em tempo real aos dados mais recentes
- **Escalabilidade**: Suporte a grandes volumes de dados
- **Segurança**: Conexão SSL/TLS com autenticação segura

### Configuração da Conexão
```python
jdbc_url = "jdbc:postgresql://aws-1-sa-east-1.pooler.supabase.com:6543/postgres?sslmode=require"
db_properties = {
    "user": "postgres.gkqgjmsqisroffmbffmf",
    "password": "N`73gQ4L$*6h",
    "driver": "org.postgresql.Driver"
}
```

## Boas Práticas adotadas
- Idempotência onde possível (reexecuções não devem corromper estado).
- Separação por camadas e domínio (`automobile`).
- Parametrização e variáveis de ambiente via widgets/`spark.conf`.
- Overwrite e operações destrutivas somente quando protegidas por parâmetros.
- Conexão segura com banco de dados em nuvem via JDBC.

---
