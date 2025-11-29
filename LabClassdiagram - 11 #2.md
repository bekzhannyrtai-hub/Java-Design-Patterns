```mermaid
classDiagram
    direction TB
    
    %% Абстрактный класс/Интерфейс для общих методов (Пункт 3 требований)
    class SystemUser {
        <<abstract>>
        +int ID
        +String Name
        +void UpdateData()
    }
    
    %% Наследование (Пункт 2, 3 требований)
    SystemUser <|-- Patient
    SystemUser <|-- Doctor
    
    %% Основные классы и их атрибуты/методы
    
    class Patient {
        +String DateOfBirth
        +String Address
        +String MedicalHistory
        +RegisterForAppointment()
        +ViewHistory()
    }
    
    class Doctor {
        +String Specialization
        +String Schedule
        +String Cabinet
        +AssignTreatment()
        +PrescribeMedication()
        +UpdateSchedule()
    }

    class Appointment {
        +Date Date
        +Time Time
        +String Status %% Planned, Canceled, Completed
        +Create()
        +Cancel()
        +Complete()
    }
    
    class MedicalRecord {
        +List<Appointment> AppointmentRecords
        +List<String> ExamResults
        +AddEntry()
        +UpdateDiagnosis()
        +DeleteEntry()
    }
    
    class Prescription {
        +String Medicine
        +String Dosage
        +Date ExpirationDate
        +Create()
        +Update()
        +Annul()
    }
    
    class Medication {
        +String Name
        +int Quantity
        +Date ExpirationDate
        +Order()
        +Issue()
        +WriteOff()
    }
    
    %% Ассоциации (Пункт 2 требований)
    Patient "1" -- "1" MedicalRecord : имеет (один-к-одному)
    MedicalRecord "1" -- "*" Appointment : содержит (один-ко-многим)
    Patient "1" -- "*" Appointment : записывается (один-ко-многим)
    Doctor "1" -- "*" Appointment : проводит (один-ко-многим)
    Doctor "1" -- "*" Prescription : выписывает
    Patient "1" -- "*" Prescription : получает
    Medication "*" -- "*" Prescription : используется в (многие-ко-многим)
