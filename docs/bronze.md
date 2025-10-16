# Camada Bronze

A **Camada Bronze** é responsável pela **ingestão dos dados brutos** exatamente como são recebidos das fontes.

## Principais Características

- Dados não tratados.  
- Armazenados em formato **Delta**.  
- Mantém o histórico completo de ingestões.  
- Fonte única de verdade dos dados originais.

## Exemplo de Processamento

Os notebooks do Databricks nesta camada realizam:
- Leitura de arquivos CSV, JSON ou Parquet.  
- Aplicação de schema explícito (quando necessário).  

## Resultado

Ao final, os dados brutos ficam disponíveis para tratamento na camada Silver.
