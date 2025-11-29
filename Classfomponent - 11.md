```mermaid
C4Component
    title UML Component Diagram for Online Banking System
    
    Component(Frontend, "Frontend", "Web and Mobile Application", "Provides user interaction.") [cite: 88, 89]
    Component(Backend, "Backend", "Server Logic", "Handles application logic and request routing.") [cite: 90]
    Component(Database, "Database", "Data Storage", "Stores information about clients, accounts, and transactions.") [cite: 91]
    Component(AuthService, "Authorization System", "User Management", "Handles user authorization and authentication.") [cite: 92]
    Component(PaymentGateway, "Payment Gateway", "Transfer Processing", "Facilitates payments and transfers.") [cite: 93]
    Component(NotificationService, "Notification System", "SMS/Email", "Sends SMS and email notifications to clients.") [cite: 94]
    Component(AnalyticsModule, "Analytics Module", "Reports and Statistics", "Processes data from the database and generates reports.") [cite: 95, 108]
    Component(MonitoringSystem, "Monitoring System", "System Status Tracking", "Checks availability and performance of all components.") [cite: 96, 109]
    
    System_Ext(ExternalBanks, "External Banks", "External API")
    System_Ext(ServiceProviders, "Service Providers", "External API")
    
    Rel(Frontend, Backend, "Interaction", "REST API / GraphQL") [cite: 99]
    Rel(Backend, Database, "Retrieve/Update data", "SQL") [cite: 101, 102, 131]
    Rel(Backend, AuthService, "Check access rights", "Token Authentication") [cite: 106, 138]
    Rel(Backend, PaymentGateway, "Initiate payments", "External API")
    Rel(Backend, NotificationService, "Send notifications", "Internal API") 
    
    Rel(PaymentGateway, ExternalBanks, "Transfers", "External API") [cite: 104]
    Rel(PaymentGateway, ServiceProviders, "Service payments", "External API") [cite: 104]

    Rel(AnalyticsModule, Database, "Retrieve data for analysis", "SQL") [cite: 108]
    Rel(MonitoringSystem, Backend, "Check availability", "HTTP") [cite: 109]
    Rel(MonitoringSystem, Database, "Check status", "SQL") [cite: 109]
    Rel(MonitoringSystem, AuthService, "Check status", "HTTP") [cite: 109]
