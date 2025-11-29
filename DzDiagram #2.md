```mermaid
classDiagram
    direction LR

    %% Определяем Компоненты как Классы
    class Backend
    class Database
    class RouteOptimizationModule
    class WarehouseManagementModule
    class CourierIntegrationModule
    class NotificationSystem
    class AnalyticsSystem
    class Frontend
    class MobileApp

    %% Определяем Внешние Системы
    class ExternalCourierServicesAPI
    class PaymentGateway

    %% Добавляем стереотипы для ясности (<<Component>>)
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
    
    %% Описываем Взаимодействия (Associations)
    
    %% Frontend interactions (REST API / WebSockets)
    Frontend -- Backend : Client Requests (REST API)
    MobileApp -- Backend : Courier Data (REST API / WS)

    %% Backend and Core Logic interactions
    Backend --> Database : Read/Write Data (SQL)
    Backend --> RouteOptimizationModule : Optimization Request (gRPC)
    Backend --> WarehouseManagementModule : Inventory Management (API)
    Backend --> CourierIntegrationModule : Delivery Management
    Backend --> NotificationSystem : Notification Trigger
    Backend --> PaymentGateway : Transaction Processing

    %% Module and External System interactions
    
    CourierIntegrationModule -- ExternalCourierServicesAPI : Send/Receive Statuses (API)
    ExternalCourierServicesAPI --> CourierIntegrationModule : Status Webhooks

    NotificationSystem .-> Frontend : Notifications to Clients
    NotificationSystem .-> MobileApp : Notifications to Couriers

    AnalyticsSystem <.. Backend : Collect Delivery Data
    AnalyticsSystem --> Database : Read Data for Reports
