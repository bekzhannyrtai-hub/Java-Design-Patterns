```mermaid
graph TB
    subgraph "Система онлайн-банкинга"
        UI[<b>User Interface</b><br/>Веб-интерфейс и мобильное приложение]
        
        AC[<b>AccountController</b><br/>Управление счетами]
        TC[<b>TransferController</b><br/>Обработка переводов]
        RC[<b>ReportController</b><br/>Генерация отчетов]
        AC[<b>AuthController</b><br/>Аутентификация]
        
        DB[(<b>Database</b><br/>Хранилище данных)]
    end
    
    %% Взаимодействия
    UI -->|"login(), logout()"| AC
    UI -->|"createAccount(), getBalance()"| AC
    UI -->|"transferFunds(), getTransactions()"| TC
    UI -->|"generateStatement(), getReport()"| RC
    
    AC -->|"storeAccountData(), queryAccounts()"| DB
    TC -->|"recordTransaction(), updateBalances()"| DB
    RC -->|"queryTransactions(), getHistory()"| DB
    AC -->|"verifyUser(), storeSession()"| DB
    
    AC -->|"getAccountInfo()"| TC
    TC -->|"getTransactionData()"| RC
    
    %% Интерфейсы
    subgraph "Интерфейсы (Ports)"
        I1[IAccountService]
        I2[ITransferService]
        I3[IReportService]
        I4[IAuthService]
    end
    
    style UI fill:#e1f5fe
    style AC fill:#e8f5e8
    style TC fill:#fff3e0
    style RC fill:#f3e5f5
    style AC fill:#fce4ec
    style DB fill:#ffecb3
