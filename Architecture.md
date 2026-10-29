# Main Architecture

The project follows a multi-service backend architecture.

Different services are responsible for different tasks, such as API handling, fast data fetching, real-time communication, and AI processing.
```  
                         MyBlog
                           |
                    React Frontend
                           |
                    API Communication
                           |
                    Node.js / Express
                           |
        ┌──────────────────┼───────────────────────────────────────┐
        |                  |                  |                    |
        |                 Kafka               Redis               BullMq
        |                  |                  |                    |
        |              Event Messaging       Cache            Background Queue processing
        |                  |                 
    ┌───|                  |
    ┌──────────────────────┴─────────────────┐
    |                      |                 |
  MongoDB              Python AI        Other Services
    |                  Moderation            |
Persistent                                   |   
Storage                             Rust Axum API, Elixir Phoenix Chat
```

<h2><b> *More details will be added as the documentation progresses.* </b></h2>



```mermaid
graph TD
    %% Styling Classes
    classDef client fill:#f9f,stroke:#333,stroke-width:2px;
    classDef gateway fill:#bbf,stroke:#333,stroke-width:2px;
    classDef broker fill:#fbb,stroke:#333,stroke-width:2px;
    classDef worker fill:#bfb,stroke:#333,stroke-width:2px;
    classDef db fill:#fff,stroke:#333,stroke-width:2px;

    %% Web Client Tier
    subgraph Web_Client [Web Client Tier - Browser Sandbox]
        React[React Frontend App]:::client
        PhoenixClient[Phoenix Socket Client]:::client
        SocketIOClient[Socket.IO Client]:::client
    end

    %% External Infrastructure
    ImageKit[ImageKit Cloud Storage]:::db

    %% Request Ingestion
    MainAPI[Main API Gateway<br>Node.js / Express]:::gateway
    AuthMidd[Token Management /<br>Auth Middleware]:::gateway
    AxumFetch[Rust Axum Fetch API]:::gateway

    %% Event Broker
    Kafka[Apache Kafka Cluster]:::broker

    %% Fallback Mechanisms
    RedisQueue[Local Redis Queue]:::db
    BullMQ[BullMQ Worker Service]:::worker

    %% Downstream Processing Consumers
    TSWorker[TS Ingestion Worker]:::worker
    PythonAI[Python AI Moderation]:::worker

    %% Primary Storage
    MongoDB[(MongoDB Database)]:::db

    %% Component Interconnections
    React -->|1. Direct Upload| ImageKit
    ImageKit -.->|2. Returns Asset URL| React
    
    React -->|3. HTTP/REST POST| MainAPI
    React -->|Public HTTP GET| AxumFetch
    AxumFetch -->|High-Perf Read Only| MongoDB

    MainAPI -->|Auth Verification Trigger| AuthMidd
    AuthMidd -->|Read Lookup Data| MongoDB

    SocketIOClient <-->|Live System State Updates| MainAPI
    PhoenixClient <-->|Live Ephemeral/Persistent Chat| Phoenix[Elixir Phoenix Engine]:::gateway
    Phoenix -->|Stream Durable Chat Logs| Kafka

    MainAPI -->|4. Publish Event Payload| Kafka
    MainAPI -.->|Kafka Offline Fallback| RedisQueue
    RedisQueue -->|Jobs from Redis| BullMQ
    BullMQ -->|Direct Failover Write| MongoDB

    Kafka -->|Consume Streams| TSWorker
    Kafka -->|Consume Streams| PythonAI

    TSWorker -->|Idempotent DB Upsert| MongoDB
    PythonAI -->|Local HuggingFace Inference| MongoDB
```

