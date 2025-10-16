# Camada Bronze

A **Camada Bronze** é responsável pela **ingestão dos dados brutos** diretamente do banco PostgreSQL em nuvem (Supabase).

## Conexão com Banco de Dados

A ingestão é realizada através de conexão JDBC direta com o Supabase:

```python
spark = SparkSession.builder.appName("AutomobileBronze").getOrCreate()

jdbc_url = (
    "jdbc:postgresql://aws-1-sa-east-1.pooler.supabase.com:6543/postgres"
    "?sslmode=require&sslfactory=org.postgresql.ssl.NonValidatingFactory"
)

db_properties = {
    "user": "postgres.gkqgjmsqisroffmbffmf",           
    "password": "N`73gQ4L$*6h",         
    "driver": "org.postgresql.Driver",
}

df_auto = spark.read.jdbc(url=jdbc_url, table="automobile", properties=db_properties)
```

## Principais Características

- Dados não tratados.  
- Armazenados em formato **Delta**.  
- Mantém o histórico completo de ingestões.  
- Fonte única de verdade dos dados originais.

## Processamento

Os notebooks do Databricks nesta camada realizam:
- Conexão direta com banco PostgreSQL via JDBC
- Leitura de tabelas específicas (automobile, motor, dimensoes, origem, ano_modelo)
- Aplicação de metadados de auditoria (timestamp, nome da fonte)
- Persistência em formato Delta Lake  

## Resultado

Ao final, os dados brutos ficam disponíveis para tratamento na camada Silver.
