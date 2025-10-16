# Arquitetura do Projeto

O pipeline segue a **Arquitetura Medalhão**, com três camadas principais:

1. **Bronze:** ingestão de dados diretamente do banco PostgreSQL em nuvem (Supabase).  
2. **Silver:** limpeza, padronização e integração de dados.  
3. **Gold:** agregação, enriquecimento e modelagem dimensional final.

## Tecnologias Utilizadas

- **Databricks**: notebooks, Delta Lake, volumes de dados.
- **PySpark**: processamento e transformação.
- **SQL**: criação de schemas, tabelas e merges.
- **PostgreSQL (Supabase)**: banco de dados em nuvem como fonte principal de dados.
- **JDBC**: conectividade para ingestão direta do banco.
- **Delta Tables**: persistência de cada camada.
- **Git**: versionamento do código.

## Fonte de Dados

O pipeline utiliza **PostgreSQL hospedado no Supabase** como fonte principal de dados, oferecendo:

- **Conectividade em tempo real**: Acesso direto via JDBC
- **Dados sempre atualizados**: Elimina latência de arquivos
- **Segurança**: Conexão SSL/TLS com autenticação
- **Escalabilidade**: Suporte a grandes volumes de dados

## Benefícios

- Histórico completo de dados brutos.
- Padronização e governança.
- Dados prontos para análise e dashboards.
- Escalabilidade e rastreabilidade.