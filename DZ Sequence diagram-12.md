```mermaid
sequenceDiagram
    actor Client
    participant System
    participant PaymentGateway
    participant Administrator
    participant Contractors
    participant Manager

    %% Stage 1: Booking Request
    Client->>System: Check venue availability
    activate System
    System-->>Client: Response: availability, cost
    deactivate System

    alt Venue is available
        Client->>System: Confirm booking
        activate System
        System->>PaymentGateway: Request advance payment
        
        alt Payment successful
            PaymentGateway-->>System: Payment confirmation
            System->>Client: Notification: Booking confirmed
            System->>Administrator: Notification: New booking
            deactivate System
            
            %% Stage 3: Event Organization
            Administrator->>Administrator: Prepare task list
            par Parallel notifications
                Administrator->>Contractors: Task notification
            and
                Administrator->>Contractors: Task notification
            end
            
            Contractors-->>Administrator: Completion confirmation
            Administrator->>System: Readiness report
            
            %% Stage 4: Event Completion
            System->>Client: Request service quality evaluation
            Client-->>System: Event feedback
            System->>Manager: Report with feedback
            
        else Payment declined
            PaymentGateway-->>System: Payment error
            System->>Client: Notification: Please retry payment
            deactivate System
        end
        
    else Venue is unavailable
        System->>Client: Suggest alternative date/venue
    end
