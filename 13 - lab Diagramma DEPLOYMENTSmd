```mermaid
graph TB
    CA1[Клиент 1<br/>Browser]
    CA2[Клиент 2<br/>Mobile]
    CA3[Клиент 3<br/>Desktop]
    
    LB[Load Balancer]
    WAF[WAF]
    
    WS1[Web Server 1]
    WS2[Web Server 2]
    
    AS1[App Server 1<br/>Spring Boot]
    AS2[App Server 2<br/>Spring Boot]
    
    PS[Payment Service]
    DS[Delivery Service]
    NS[Notification Service]
    
    PrimaryDB[Primary DB<br/>PostgreSQL]
    ReplicaDB[Replica DB]
    Cache[Cache<br/>Redis]
    
    CA1 --> LB
    CA2 --> LB
    CA3 --> LB
    
    LB --> WAF
    WAF --> WS1
    WAF --> WS2
    
    WS1 --> AS1
    WS2 --> AS2
    
    AS1 --> PS
    AS1 --> DS
    AS1 --> NS
    AS2 --> PS
    AS2 --> DS
    AS2 --> NS
    
    AS1 --> PrimaryDB
    AS2 --> PrimaryDB
    PS --> PrimaryDB
    DS --> PrimaryDB
    
    PrimaryDB --> ReplicaDB
    AS1 --> Cache
    AS2 --> Cache
    
    style CA1 fill:#e1f5fe
    style LB fill:#ffecb3
    style WAF fill:#ffcdd2
    style WS1 fill:#e8f5e8
    style AS1 fill:#f3e5f5
    style PrimaryDB fill:#fff3e0
    style PS fill:#c8e6c9
    style DS fill:#bbdefb
    style NS fill:#f0f4c3
