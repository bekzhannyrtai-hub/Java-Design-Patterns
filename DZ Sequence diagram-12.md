```mermaid
sequenceDiagram
    actor Client
    participant System
    participant PaymentGateway
    participant Administrator
    participant Contractors
    participant Manager

    Note over Client,System: Stage 1: Booking Request
    Client->>System: Check venue availability
    System-->>Client: Response: availability, cost

    alt Venue is available
        Client->>System: Confirm booking
        System->>PaymentGateway: Request advance payment
        
        alt Payment successful
            PaymentGateway-->>System: Payment confirmation
            System->>Client: Notification: Booking confirmed
            System->>Administrator: Notification: New booking
        else Payment declined
            PaymentGateway-->>System: Payment error
            System->>Client: Notification: Please retry payment
        end
    else Venue is unavailable
        System->>Client: Suggest alternative date/venue
    end

    Note over Administrator,Contractors: Stage 3: Event Organization
    Administrator->>Administrator: Prepare task list
    par Parallel notifications to contractors
        Administrator->>Contractors: Task notification 1
        Administrator->>Contractors: Task notification 2
    end
    Contractors-->>Administrator: Completion confirmation
    Administrator->>System: Readiness report

    Note over Client,Manager: Stage 4: Event Completion
    System->>Client: Request service quality evaluation
    Client-->>System: Event feedback
    System->>Manager: Report with feedback
