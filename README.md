

flowchart TD
    %% Clientes
    subgraph Client_Layer [Capa de Presentación]
        A[Web Admin Panel] 
        B[Mobile / PWA Client]
    Conclusion

    %% Componentes Backend
    subgraph Backend_Ecosystem [Core de Servicios]
        C[API Gateway / PHP Backend Auth & Analytics]
        D[Go Ingestion Worker High-Throughput]
    end

    %% Almacenamiento
    subgraph Data_Layer [Capa de Persistencia]
        E[(MySQL Production Cluster)]
    end

    %% Flujos de Red
    A & B -->|REST APIs / JSON| C
    B -->|Async Queries| D
    C -->|ORM / Prepared Statements| E
    D -->|Connection Pooling| E

    %% Entrada Externa
    F[External Webhooks / Payment Notifications] -->|Payload Webhook| D
