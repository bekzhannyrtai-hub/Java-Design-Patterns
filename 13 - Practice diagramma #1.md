```mermaid
graph TB
    subgraph "CRM Система управления клиентами"
        UI[Компонент: UserInterface<br/>Предоставляет интерфейс пользователя]
        
        CC[Компонент: ClientController<br/>Управление клиентами]
        TC[Компонент: TaskController<br/>Управление задачами]
        RC[Компонент: ReportController<br/>Генерация отчетов]
        
        DB[(База данных<br/>Хранение данных)]
    end
    
    UI -->|"addClient(), getClients()"| CC
    UI -->|"addTask(), completeTask()"| TC
    UI -->|"generateReport()"| RC
    
    CC -->|"saveClient(), updateClient()"| DB
    TC -->|"saveTask(), updateTask()"| DB
    RC -->|"queryData()"| DB
    
    CC -->|"getClientData()"| RC
    TC -->|"getTaskData()"| RC
    
   
    subgraph UI
        direction LR
        UIP1[Порт: ClientOperations]
        UIP2[Порт: TaskOperations]
        UIP3[Порт: ReportOperations]
    end
    
    style UI fill:#e1f5fe
    style CC fill:#e8f5e8
    style TC fill:#fff3e0
    style RC fill:#f3e5f5
    style DB fill:#fce4ec
