```mermaid
graph TB
    UI2[UserInterface<br/>Магазин]
    
    OC[OrderController<br/>Заказы]
    PC[PaymentController<br/>Платежи]
    DC[DeliveryController<br/>Доставка]
    IC[InventoryController<br/>Склад]
    
    DB2[(Database<br/>Заказы/Товары)]
    
    UI2 --> OC
    UI2 --> PC
    UI2 --> DC
    
    OC --> DB2
    PC --> DB2
    DC --> DB2
    IC --> DB2
    
    OC --> IC
    OC --> PC
    OC --> DC
    PC --> OC
    DC --> OC
    
    style UI2 fill:#e1f5fe
    style OC fill:#e8f5e8
    style PC fill:#fff3e0
    style DC fill:#f3e5f5
    style IC fill:#ffecb3
    style DB2 fill:#fce4ec
