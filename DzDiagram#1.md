```mermaid
classDiagram
    direction LR

    class User {
        <<Abstract>>
        +int ID
        +String name
        +String email
        +String address
        +String phone
        +String role
        +register()
        +login()
        +updateData()
    }

   
    class Client {
        -int loyaltyPoints
        +placeOrder()
    }
    class Administrator {
        +manageProducts()
        +viewReports()
    }
    Client --|> User : inherits
    Administrator --|> User : inherits

 
    class Product {
        +int ID
        +String name
        +String description
        +double price
        -int quantityInStock
        +create()
        +update()
        +delete()
    }
    class Category {
        +int ID
        +String name
    }
    class Order {
        +int ID
        +LocalDate dateCreated
        +String status
        +double amount
        -String promoCode
        +process()
        +cancel()
        +pay()
    }
    class Delivery {
        +int ID
        +String address
        +String deliveryStatus
        +String courier
        +dispatch()
        +track()
        +complete()
    }
    class Payment {
        +int ID
        +String type
        +double amount
        +String status
        +LocalDate date
        +processPayment()
        +refund()
    }
    class Review {
        +int ID
        +int rating
        +String text
    }
    class Cart {
        +int ID
        +double totalCost
        +addItem(Product)
        +removeItem(Product)
        +calculateTotal()
    }


    Client "1" -- "1" Cart : has
    Client "1" -- "0..*" Order : makes
    Client "1" -- "0..*" Review : leaves

    Order "1" -- "1" Delivery : associated_with
    Order "1" -- "1" Payment : includes
    Order "1" -- "1..*" Product : contains

    Cart "1" -- "0..*" Product : contains

    Product "0..*" -- "1" Category : belongs_to
    Product "0..*" -- "0..*" Review : has

    %% Additional
    Administrator ..> Product : manages
    Order ..> Review : can_be_reviewed
