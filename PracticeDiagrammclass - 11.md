```mermaid
classDiagram
    direction LR

    class User
    class Client
    class Administrator

    abstract class Payment
    class CardPayment
    class WalletPayment
    
    class Product 
    class Category
    class Order
    class Delivery
    class Courier
    class Review
    class OrderItem
    
    User : - id: int
    User : + register()
    
    Client : - loyaltyPoints: int
    
    User <|-- Client
    User <|-- Administrator

    Payment : + process()
    Payment <|-- CardPayment
    Payment <|-- WalletPayment

    Product : + getFinalPrice(): double
    Order : + checkout()
    
    Client "1" --> "0..*" Order : places
    Order "1" *-- "1..*" OrderItem : contains
    OrderItem "0..*" --> "1" Product : relates_to
    Order "1" --> "1" Delivery : linked_to
    Delivery "1" --> "1" Courier : assigned
    Order "0..*" --> "1" Payment : paid_via
    Client "1" --> "0..*" Review : leaves
    Review "0..*" --> "1" Product : describes
    Product "0..*" --> "1" Category : belongs_to
