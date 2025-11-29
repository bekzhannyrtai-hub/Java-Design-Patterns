```mermaid
componentDiagram
    %% Компоненты системы
    component UserService {
        interface IUserService
    }

    component ProductService {
        interface IProductService
    }

    component OrderService {
        interface IOrderService
    }

    component PaymentService {
        interface IPaymentService
    }

    component NotificationService {
        interface INotificationService
    }

    %% Зависимости между компонентами
    OrderService --|> UserService : uses IUserService
    OrderService --|> ProductService : uses IProductService
    OrderService --|> PaymentService : uses IPaymentService
    PaymentService --|> NotificationService : uses INotificationService
    OrderService --|> NotificationService : uses INotificationService
