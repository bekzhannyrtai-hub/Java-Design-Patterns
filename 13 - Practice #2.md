```mermaid
graph TB
    subgraph "Узел: Клиентские устройства"
        CA[<<device>> <br/>Клиентское приложение<br/>Web/Desktop/Mobile]
    end
    
    subgraph "Центр обработки данных"
        subgraph "Узел: Сервер приложений"
            AS[<<execution environment>> <br/>Application Server<br/>Tomcat/Spring Boot]
        end
        
        subgraph "Узел: Сервер БД"
            DB[<<database>> <br/>Database Server<br/>PostgreSQL/MySQL]
        end
        
        subgraph "Узел: Платежный сервер"
            PS[<<execution environment>> <br/>Payment Server<br/>Обработка платежей]
        end
        
        subgraph "Узел: Сервер доставки"
            DS[<<execution environment>> <br/>Delivery Server<br/>Управление доставкой]
        end
    end
    
    CA -- "HTTP/HTTPS<br/>REST API" --> AS
    AS -- "JDBC<br/>ORM (Hibernate)" --> DB
    AS -- "SOAP/REST<br/>Payment API" --> PS
    AS -- "REST API<br/>Delivery Service" --> DS
    
    subgraph AS
        OS[Компонент: OrderService]
        PS[Компонент: ProductService]
        US[Компонент: UserService]
    end
    
    subgraph PS
        PC[Компонент: PaymentProcessor]
        VP[Компонент: ValidationService]
    end
    
    CA -.->|"Зависит от"| A1[Artifact: client-app.jar]
    AS -.->|"Развернут"| A2[Artifact: shop-backend.war]
    
    style CA fill:#e1f5fe
    style AS fill:#e8f5e8
    style DB fill:#fce4ec
    style PS fill:#fff3e0
    style DS fill:#f3e5f5
