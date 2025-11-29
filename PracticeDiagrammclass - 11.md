```mermaid
classDiagram
    direction LR
    
    %% -------------------- ABSTRACT ENTITIES AND INHERITANCE --------------------
    
    abstract class User {
        - id: int
        - name: String
        - email: String
        - address: String
        # role: String
        + register()
        + login()
        + updateData()
    }

    class Client {
        - loyaltyPoints: int
        + addLoyaltyPoints(points: int)
        + leaveReview()
    }

    class Administrator {
        + logAction(action: String)
        + manageProducts()
    }

    User <|-- Client
    User <|-- Administrator

    abstract class Payment {
        - id: int
        - amount: double
        - status: String
        + process()
        + refund()
    }

    class CardPayment
    class WalletPayment

    Payment <|-- CardPayment
    Payment <|-- WalletPayment

    %% -------------------- CORE ENTITIES --------------------
    
    class Product {
        - id: int
        - name: String
        - price: double
        - stockQuantity: int
        - discount: double
        + getFinalPrice(): double
        + create()
        + update()
    }
    
    class Category {
        - id: int
        - name: String
    }
    
    class Order {
        - id: int
        - creationDate: Date
        - status: Status (CREATED, DELIVERED, CANCELED)
        - total: double
        - promoCode: String
        + checkout()
        + cancel()
        + pay()
        + calculateTotal()
    }
    
    class Delivery {
        - id: int
        - address: String
        - status: String
        + dispatch()
        + track()
        + complete()
    }
    
    class Courier {
        - name: String
        + startDelivery()
    }
    
    class Review {
        - rating: int
        - comment: String
    }
    
    %% -------------------- ASSOCIATIVE CLASS --------------------
    
    class OrderItem {
        - quantity: int
    }
    
    %% -------------------- RELATIONSHIPS (ASSOCIATIONS) --------------------
    
    Client "1" --> "0..*" Order : places
    
    Order "1" --> "1" Delivery : linked_to
    Delivery "1" --> "1" Courier : assigned
    
    Order "1" *-- "1..*" OrderItem : contains
    OrderItem "0..*" --> "1" Product : relates_to

    Product "0..*" --> "1" Category : belongs_to
    
    Order "0..*" --> "1" Payment : paid_via
    
    Client "1" --> "0..*" Review : leaves
    Review "0..*" --> "1" Product : describes
