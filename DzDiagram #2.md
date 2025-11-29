```mermaid
classDiagram
    direction LR

    class Backend
    class Database
    class RouteOptimizationModule
    class WarehouseManagementModule
    class CourierIntegrationModule
    class NotificationSystem
    class AnalyticsSystem
    class Frontend
    class MobileApp

    class ExternalCourierServicesAPI
    class PaymentGateway

    %% Стереотипы для обозначения типа компонента
    Backend: <<Component>>
    Database: <<Component>>
    RouteOptimizationModule: <<Component>>
    WarehouseManagementModule: <<Component>>
    CourierIntegrationModule: <<Component>>
    NotificationSystem: <<Component>>
    AnalyticsSystem: <<Component>>
    Frontend: <<Client>>
    MobileApp: <<Client>>
    ExternalCourierServicesAPI: <<External>>
    PaymentGateway: <<External>>
    
    %% Взаимодействия Frontend (Solid Line)
    Frontend --> Backend : Client Requests (REST API)
    MobileApp --> Backend : Courier Data (REST API / WS)

    %% Взаимодействия Backend (Solid Line)
    Backend --> Database : Read/Write Data (SQL)
    Backend --> RouteOptimizationModule : Optimization Request (gRPC)
    Backend --> WarehouseManagementModule : Inventory Management (API)
    Backend --> CourierIntegrationModule : Delivery Management
    Backend --> NotificationSystem : Notification Trigger
    Backend --> PaymentGateway : Transaction Processing

    %% Интеграция с Внешними Службами
    CourierIntegrationModule --> ExternalCourierServicesAPI : Send/Receive Statuses (API)
    ExternalCourierServicesAPI --> CourierIntegrationModule : Status Webhooks

    %% Уведомления (Dashed Line, самая безопасная замена для Dependency)
    NotificationSystem ..> Frontend : Notifications to Clients
    NotificationSystem ..> MobileApp : Notifications to Couriers

    %% Аналитика
    Backend ..> AnalyticsSystem : Supplies Delivery Data
    AnalyticsSystem --> Database : Read Data for Reports
