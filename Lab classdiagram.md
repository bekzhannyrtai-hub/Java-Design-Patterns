```meirmaid
classDiagram
    direction LR
    
    class Book {
        +String Title
        +String Author
        +String ISBN
        +Boolean IsAvailable
        +MarkAsLoaned()
        +MarkAsAvailable()
    }
    
    class Reader {
        +int Id
        +String Name
        +String Email
        +BorrowBook(Book)
        +ReturnBook(Book)
    }
    
    class Librarian {
        +int Id
        +String Name
        +String Position
        +AddBook(Book)
        +RemoveBook(Book)
    }
    
    class Loan {
        +Date LoanDate
        +Date ReturnDate
        +IssueLoan()
        +CompleteLoan()
    }
    
    %% Ассоциации
    Loan "1" -- "1" Book : регистрирует >
    Loan "1" -- "1" Reader : для >
    Reader "1" -- "*" Loan : имеет много
    Book "1" -- "*" Loan : может быть во многих
    Librarian --> Reader : управляет
    Librarian --> Book : управляет
