```meirmaid
classDiagram
    direction TB
    
    %% Абстрактный класс или Интерфейс для общих методов
    class SystemUser {
        <<abstract>>
        +int ID
        +String Name
        +void UpdateData()
    }
    
    %% Классы, наследующие от SystemUser
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
    
    SystemUser <|-- Patient
    SystemUser <|-- Doctor

    %% Основные классы
    class Appointment {
        +Date Date
        +Time Time
        +String Status %% Planned, Canceled, Completed [cite: 94, 125, 126]
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
    
    %% Ассоциации
    Patient "1" -- "1" MedicalRecord : имеет > [cite: 114]
    MedicalRecord "1" -- "*" Appointment : содержит > [cite: 115]
    Patient "1" -- "*" Appointment : записывается > [cite: 112]
    Doctor "1" -- "*" Appointment : проводит > [cite: 113]
    Doctor "1" -- "*" Prescription : выписывает
    Patient "1" -- "*" Prescription : получает
    Medication "*" -- "*" Prescription : используется в > [cite: 116]
