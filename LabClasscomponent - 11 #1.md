```mermaid
componentDiagram
    direction TB
    
    component UserService {
        interface IUserService
    }
    
    component ProductService {
        interface IProductService
    }
    
    component PaymentService {
        interface IPaymentService
    }
    
    component NotificationService {
        interface INotificationService
    }
    
    component OrderService {
        interface IOrderService
    }
    
    %% Связи: OrderService требует другие интерфейсы
    OrderService "1" --o IProductService : Requires Product Info
    OrderService "1" --o IPaymentService : Requires Payment Processing
    OrderService "1" --o IUserService : Requires User Details
    OrderService "1" --o INotificationService : Requires Notifications
    
    %% Реализация интерфейсов
    IUserService ..> UserService
    IProductService ..> ProductService
    IPaymentService ..> PaymentService
    INotificationService ..> NotificationService
    IOrderService ..> OrderService
