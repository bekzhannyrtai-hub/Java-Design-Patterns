```mermaid
componentDiagram
    [UserService] --> [IUserService] : Provides
    [ProductService] --> [IProductService] : Provides
    [OrderService] --> [IOrderService] : Provides
    [PaymentService] --> [IPaymentService] : Provides
    [NotificationService] --> [INotificationService] : Provides
    
    %% Зависимости (OrderService требует интерфейсы)
    [OrderService] --o [IProductService] : Requires
    [OrderService] --o [IPaymentService] : Requires
    [OrderService] --o [IUserService] : Requires
    [OrderService] --o [INotificationService] : Requires
    
    %% Реализация интерфейсов
    [IProductService] ..> [ProductService] : Realizes
    [IPaymentService] ..> [PaymentService] : Realizes
    [IUserService] ..> [UserService] : Realizes
    [INotificationService] ..> [NotificationService] : Realizes
