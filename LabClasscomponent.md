```mermaid
graph TD
    subgraph Внутренние компоненты
        UM[UserManagement<br/>UserManagementAPI]
        OM[OrderManagement<br/>OrderManagementAPI]
        RP[RoutePlanner<br/>RoutePlannerAPI]
        VM[VehicleMonitoring<br/>MonitoringAPI]
        PM[PaymentManagement<br/>PaymentAPI]
        NT[NotificationService<br/>NotificationAPI]
    end
    
    subgraph Внешние системы
        MS[MapService<br/>MapServiceAPI]
        PG[PaymentGateway<br/>PaymentGatewayAPI]
        GPS[GPSSystem<br/>GPSAPI]
        SMS[SMSService<br/>SMSAPI]
        ES[EmailService<br/>EmailAPI]
    end
    
    %% Взаимосвязи
    OM -->|uses| UM
    OM -->|uses| RP
    RP -->|uses| MS
    VM -->|uses| GPS
    PM -->|uses| PG
    NT -->|uses| SMS
    NT -->|uses| ES
    
    UM -->|
