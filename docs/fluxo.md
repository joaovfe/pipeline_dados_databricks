# Fluxo das Camadas do Pipeline

**Exemplificação do fluxo entre camadas:**

    A[Landing / Dados Brutos] --> B[Camada Bronze]
    B --> C[Camada Silver]
    C --> D[Camada Gold]
    
    subgraph Bronze
        B1[bronze.automobile]
        B2[bronze.motor]
        B3[bronze.dimensoes]
        B4[bronze.origem]
        B5[bronze.ano_modelo]
    end
    
    subgraph Silver
        S1[silver.automobile]
        S2[silver.motor]
        S3[silver.dimensoes]
        S4[silver.origem]
        S5[silver.ano_modelo]
    end
    
    subgraph Gold
        G1[dim_automobile]
        G2[dim_motor]
        G3[dim_dimensoes]
        G4[dim_origem]
        G5[dim_ano_modelo]
    end
