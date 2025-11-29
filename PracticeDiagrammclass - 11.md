```mermaid
classDiagram
    direction LR
    
    %% Inheritance
    class User {
        -int id
        -string firstName
        -string lastName
        -string login
        -string password
    }
    class Administrator {
        +manageStructures()
        +manageUsers()
    }
    class Student {
        -string recordBookNumber
        -list<Course> courseList
        +registerForCourse()
        +viewGrades()
    }
    class Professor {
        -list<Course> courseList
        -string position
        +conductClass()
        +setGrade()
        +manageSchedule()
    }

    User <|-- Administrator : Inheritance
    User <|-- Student : Inheritance
    User <|-- Professor : Inheritance

    %% Aggregation and Composition
    class University {
        -string name
        -string address
        -list<Faculty> facultyList
        +addFaculty()
        +removeFaculty()
    }
    class Faculty {
        -string name
        -list<Department> departmentList
        +addDepartment()
        +removeDepartment()
    }
    class Department {
        -string name
        -list<Professor> professorList
        -list<Course> courseList
        +addProfessor()
        +removeProfessor()
    }

    University *-- "1" Faculty : contains 1..*
    Faculty *-- "1" Department : contains 1..*
    Department "1" -- "0..*" Professor : isAssignedTo
    Department "1" -- "0..*" Course : isAssignedTo
    
    %% Associations
    class Course {
        -string name
        -Department department
        -list<Student> studentList
        -Schedule schedule
        +addStudent()
        +removeStudent()
    }
    class Schedule {
        -string date
        -string time
        -string classroom
        +createSchedule()
        +modifySchedule()
    }
    class Exam {
        -Course course
        -string date
        -list<Grade> gradeList
        +scheduleExam()
        +setGrade()
    }
    class Grade {
        -int value
        -Student student
        -Professor professor
        -Exam exam
    }

    Course "1" -- "1..*" Professor : isTaughtBy
    Course "1" -- "0..*" Student : enrolls 1..*
    Course "1" -- "0..*" Exam : has
    Exam "1" -- "1..*" Grade : contains
    Course "1" -- "0..*" Schedule : has
    Schedule "0..*" -- "0..*" Student : links
    Schedule "0..*" -- "0..*" Professor : links
    Student "1" -- "0..*" Grade : receives
    Professor "1" -- "0..*" Grade : sets
