# Pipeline no Databricks

O pipeline é composto por uma sequência de notebooks orquestrados para mover os dados entre as camadas.

## Etapas

1. **Preparação do ambiente:** criação dos schemas e volume de dados.
2. **Ingestão (Bronze):** leitura direta do banco PostgreSQL em nuvem (Supabase) e persistência dos dados brutos.
3. **Transformação (Silver):** limpeza e padronização.  
4. **Modelagem (Gold):** agregação e enriquecimento.  

---

## Execução no Databricks

- Cada notebook representa uma etapa da arquitetura.  
- A execução pode ser automatizada via **Jobs** ou **Workflows**.  
- Parâmetros e logs são utilizados para rastreabilidade.

---
