```mermaid
classDiagram
    %% Абстрактные классы и интерфейсы
    class Person {
        <<abstract>>
        +int ID
        +string Name
        +DateTime DateOfBirth
        +string Address
    }

    class MedicalWorker {
        <<abstract>>
        +string Specialization
        +Schedule WorkSchedule
    }

    %% Основные классы
    class Patient {
        +string MedicalHistory
        +registerForAppointment()
        +updateData()
        +viewHistory()
    }

    class Doctor {
        +string Office
        +prescribeTreatment()
        +writePrescription()
        +updateSchedule()
    }

    class Nurse {
        +string Department
        +assistDoctor()
        +administerMedication()
    }

    class Appointment {
        +int ID
        +DateTime Date
        +DateTime Time
        +string Status
        +create()
        +cancel()
        +complete()
    }

    class MedicalRecord {
        +int ID
        +List~Appointment~ Appointments
        +string ExaminationResults
        +addEntry()
        +updateDiagnosis()
        +deleteEntry()
    }

    class Prescription {
        +int ID
        +string Medication
        +string Dosage
        +DateTime ExpiryDate
        +create()
        +update()
        +cancel()
    }

    class Medication {
        +int ID
        +string Name
        +int Quantity
        +DateTime ExpiryDate
        +order()
        +dispense()
        +writeOff()
    }

    %% Наследование
    Person <|-- Patient
    Person <|-- MedicalWorker
    MedicalWorker <|-- Doctor
    MedicalWorker <|-- Nurse

    %% Ассоциации
    Patient "1" -- "*" Appointment
    Doctor "1" -- "*" Appointment
    Patient "1" -- "1" MedicalRecord
    MedicalRecord "1" -- "*" Appointment
    Doctor "1" -- "*" Prescription
    Patient "1" -- "*" Prescription
    Medication "1" -- "*" Prescription
