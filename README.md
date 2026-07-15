erDiagram
    USERS {
        uuid id PK
        string name
        string email
        string password_hash
        string role
        datetime created_at
    }
    
    DRIVERS {
        uuid id PK
        string full_name
        string cnh_number
        string phone
        string status "Disponível, Férias, etc"
    }
    
    TRUCKS {
        uuid id PK
        string plate
        string model
        int year
        string status "Disponível, Em Rota, Manutenção"
        uuid driver_id FK
    }
    
    TRIPS {
        uuid id PK
        uuid truck_id FK
        string origin
        string destination
        datetime departure_date
        datetime arrival_date
        string status "Pendente, Em Andamento, Concluída"
    }
    
    AI_CARGO_SCANS {
        uuid id PK
        uuid trip_id FK
        decimal occupancy_pct "Ex: 78.50"
        string image_url
        boolean is_anomaly
        datetime scan_timestamp
    }
    
    TELEMATICS_LOGS {
        uuid id PK
        uuid trip_id FK
        decimal latitude
        decimal longitude
        decimal speed
        datetime timestamp
    }

    %% Relacionamentos do Sistema
    DRIVERS ||--o{ TRUCKS : "conduz"
    TRUCKS ||--o{ TRIPS : "realiza"
    TRIPS ||--o{ AI_CARGO_SCANS : "monitorada_por"
    TRIPS ||--o{ TELEMATICS_LOGS : "rastreada_por"
