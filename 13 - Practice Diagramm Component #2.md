```mermaid
graph TB
    subgraph "Система управления заказами"
        UI2[<b>UserInterface</b><br/>Интернет-магазин]
        
        OC[<b>OrderController</b><br/>Управление заказами]
        PC[<b>PaymentController</b><br/>Обработка платежей]
        DC[<b>DeliveryController</b><br/>Управление доставкой]
        IC[<b>InventoryController</b><br/>Управление складом]
        
        DB2[(<b>Database</b><br/>Хранилище заказов)]
    end
    
    %% Взаимодействия
    UI2 -->|"createOrder(), viewOrders()"| OC
    UI2 -->|"processPayment()"| PC
    UI2 -->|"trackDelivery()"| DC
    
    OC -->|"saveOrder(), updateStatus()"| DB2
    PC -->|"recordPayment()"| DB2
    DC -->|"updateDeliveryStatus()"| DB2
    IC -->|"updateStock()"| DB2
    
    OC -->|"checkInventory()"| IC
    OC -->|"initiatePayment()"| PC
    OC -->|"scheduleDelivery()"| DC
    PC -->|"confirmPayment()"| OC
    DC -->|"confirmDelivery()| OC
    
    style UI2 fill:#e1f5fe
    style OC fill:#e8f5e8
    style PC fill:#fff3e0
    style DC fill:#f3e5f5
    style IC fill:#ffecb3
    style DB2 fill:#fce4ec
