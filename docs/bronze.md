# Camada Bronze

A **Camada Bronze** é responsável pela **ingestão dos dados brutos** exatamente como são recebidos das fontes.
Anteriormente, o arquivo .csv era injetado diretamente dentro do Databricks, agora a conexão é feita através do Supabase, através dp seguinte código:

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
