```mermaid
graph TB
    UI[User Interface<br/>Веб/Mobile]
    
    AC[AccountController<br/>Счета]
    TC[TransferController<br/>Переводы]
    RC[ReportController<br/>Отчеты]
    ATC[AuthController<br/>Аутентификация]
    
    DB[(Database)]
    
    UI --> AC
    UI --> TC
    UI --> RC
    UI --> ATC
    
    AC --> DB
    TC --> DB
    RC --> DB
    ATC --> DB
    
    AC --> TC
    TC --> RC
    
    style UI fill:#e1f5fe
    style AC fill:#e8f5e8
    style TC fill:#fff3e0
    style RC fill:#f3e5f5
    style ATC fill:#fce4ec
    style DB fill:#ffecb3
