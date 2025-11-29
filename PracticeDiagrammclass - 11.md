```mermaid
classDiagram
    direction TB
    title UML Class Diagram (University Management)

    %% -------------------- STRUCTURAL CLASSES (Composition) --------------------
    
    class University {
        - name: String
        - address: String
        + addFaculty()
    }
    
    class Faculty {
        - name: String
        + addDepartment()
    }

    class Department {
        - name: String
        + addProfessor()
        + addCourse()
    }
    
    University "1" *-- "1..*" Faculty : contains
    Faculty "1" *-- "1..*" Department : contains

    %% -------------------- USERS (Inheritance) --------------------
    
    abstract class User {
        - id: int
        - name: String
        - email: String
        + login()
    }
    
    class Student {
        - studentID: String
        + enrollInCourse()
        + viewGrades()
    }

    class Professor {
        - position: String
        + conductClass()
        + assignGrade()
    }
    
    class Administrator {
        + manageStructures()
    }
    
    User <|-- Student
    User <|-- Professor
    User <|-- Administrator

    %% -------------------- ACADEMIC PROCESS AND RELATIONS --------------------

    class Course {
        - title: String
        + addStudent()
    }

    class Schedule {
        - date: Date
        - time: Time
        - room: String
        + createSchedule()
    }

    class Exam {
        - date: Date
        + setExam()
    }

    class Grade {
        - score: int
        - date: Date
    }

    Department "1" *-- "1..*" Course : assigns
    Department "1" o-- "0..*" Professor : includes
    
    Professor "1..*" -- "1..*" Course : teaches
    Student "0..*" -- "0..*" Course : studies
    
    Course "1" -- "0..*" Schedule : has
    Exam "1" -- "0..*" Grade : contains
    Course "1" -- "0..*" Exam : linked_to
    Student "1" -- "0..*" Grade : receives
