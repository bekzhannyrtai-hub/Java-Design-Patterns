```mermaid
componentDiagram
    [UserService] --> [IUserService] : Provides [cite: 169]
    [ProductService] --> [IProductService] : Provides [cite: 170]
    [OrderService] --> [IOrderService] : Provides [cite: 171]
    [PaymentService] --> [IPaymentService] : Provides [cite: 172]
    [NotificationService] --> [INotificationService] : Provides [cite: 173]
    
    %% Зависимости
    [OrderService] --o [IProductService] : Requires
    [OrderService] --o [IPaymentService] : Requires
    [OrderService] --o [IUserService] : Requires
    [OrderService] --o [INotificationService] : Requires
    
    [IProductService] ..> [ProductService] : Realizes
    [IPaymentService] ..> [PaymentService] : Realizes
    [IUserService] ..> [UserService] : Realizes
    [INotificationService] ..> [NotificationService] : Realizes
