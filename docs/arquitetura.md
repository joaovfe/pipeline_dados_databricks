# Arquitetura do Projeto

O pipeline segue a **Arquitetura Medalhão**, com três camadas principais:

1. **Bronze:** ingestão de dados brutos (Landing → Bronze).  
2. **Silver:** limpeza, padronização e integração de dados.  
3. **Gold:** agregação, enriquecimento e modelagem dimensional final.

## Tecnologias Utilizadas

- **Databricks**: notebooks, Delta Lake, volumes de dados.
- **PySpark**: processamento e transformação.
- **SQL**: criação de schemas, tabelas e merges.
- **Delta Tables**: persistência de cada camada.
- **Git**: versionamento do código.

## Benefícios

- Histórico completo de dados brutos.
- Padronização e governança.
- Dados prontos para análise e dashboards.
- Escalabilidade e rastreabilidade.