```mermaid
component-beta

    component [Backend Server] as Backend
    component [Database] as DB
    component [Route Optimization Module] as RouteOpt
    component [Warehouse Management Module] as Warehouse
    component [Courier Integration Module] as CourierAPIModule
    component [Notification System] as NotifSystem
    component [Analytics System] as Analytics

    component [Web Application (Clients)] as Frontend
    component [Mobile App (Couriers)] as Mobile

    component [External Courier Services API] as ExtCourier
    component [Payment Gateway] as PaymentGateway

    Frontend --(REST API)--> Backend : Client Requests
    Mobile --(REST API / WebSockets)--> Backend : Courier Data

   
    Backend --> DB : Read/Write Data (SQL)
    Backend --> RouteOpt : Route Optimization Request (gRPC)
    Backend --> Warehouse : Inventory Management (Inventory API)
    Backend --> CourierAPIModule : Delivery Management
    Backend --> NotifSystem : Notification Trigger
    Backend --> PaymentGateway : Transaction Processing

    
    CourierAPIModule --(External API)--> ExtCourier : Send/Receive Statuses
    ExtCourier --(Webhook)--> CourierAPIModule : Status Webhooks

    NotifSystem .-> Frontend : Notifications to Clients
    NotifSystem .-> Mobile : Notifications to Couriers

    Analytics <-. Backend : Collect Delivery Data
    Analytics --> DB : Read Data for Reports
