```mermaid
C4Component
    title UML Component Diagram for Online Banking System
    
    Component(Frontend, "Frontend", "Web and Mobile Application", "Provides user interaction.")
    Component(Backend, "Backend", "Server Logic", "Handles application logic and request routing.")
    Component(Database, "Database", "Data Storage", "Stores information about clients, accounts, and transactions.")
    Component(AuthService, "Authorization System", "User Management", "Handles user authorization and authentication.")
    Component(PaymentGateway, "Payment Gateway", "Transfer Processing", "Facilitates payments and transfers.")
    Component(NotificationService, "Notification System", "SMS/Email", "Sends SMS and email notifications to clients.")
    Component(AnalyticsModule, "Analytics Module", "Reports and Statistics", "Processes data and generates reports.")
    Component(MonitoringSystem, "Monitoring System", "System Status Tracking", "Checks availability and performance of all components.")
    
    System_Ext(ExternalBanks, "External Banks", "External API")
    System_Ext(ServiceProviders, "Service Providers", "External API")
    
    Rel(Frontend, Backend, "Interaction", "REST API / GraphQL")
    Rel(Backend, Database, "Retrieve/Update data", "SQL")
    Rel(Backend, AuthService, "Check access rights", "Token Authentication")
    Rel(Backend, PaymentGateway, "Initiate payments", "External API")
    Rel(Backend, NotificationService, "Send notifications", "Internal API") 
    
    Rel(PaymentGateway, ExternalBanks, "Transfers", "External API")
    Rel(PaymentGateway, ServiceProviders, "Service payments", "External API")

    Rel(AnalyticsModule, Database, "Retrieve data for analysis", "SQL")
    Rel(MonitoringSystem, Backend, "Check availability", "HTTP")
    Rel(MonitoringSystem, Database, "Check status", "SQL")
    Rel(MonitoringSystem, AuthService, "Check status", "HTTP")
