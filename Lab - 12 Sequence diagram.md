```mermaid
sequenceDiagram
    actor User
    participant System
    participant PaymentGateway
    participant Database

    Note over User,System: Этап 1: Регистрация на курс
    User->>System: Выбрать курс
    System->>Database: Проверить доступность курса
    Database-->>System: Статус доступности
    
    alt Курс доступен
        System->>Database: Добавить пользователя в список участников
        System-->>User: Подтверждение регистрации
        
        Note over User,System: Этап 2: Оплата курса
        User->>System: Выбрать способ оплаты
        
        alt Онлайн-платеж
            System->>PaymentGateway: Запрос на обработку платежа
            PaymentGateway-->>System: Результат оплаты
            
            alt Платеж успешен
                System->>Database: Активировать доступ к курсу
                System-->>User: Доступ к курсу открыт
            else Платеж отклонен
                System-->>User: Уведомление с предложением повторить оплату
            end
            
        else Банковский перевод
            System-->>User: Инструкции для банковского перевода
            System->>Database: Ожидание подтверждения оплаты
        end
        
        Note over User,System: Этап 3: Прохождение обучения
        User->>System: Начать обучение
        loop Для каждого модуля
            User->>System: Выполнить задания и тесты
            System->>Database: Сохранить результаты
        end
        
        System->>System: Проверить итоговые результаты
        alt Результаты удовлетворительные
            System->>Database: Записать успешное завершение
            System-->>User: Выдать сертификат
        else Результаты неудовлетворительные
            System-->>User: Предложить пересдать тесты
        end
        
        Note over User,System: Этап 4: Завершение процесса
        User->>System: Скачать сертификат
        System->>Database: Сохранить данные о завершении курса
        System-->>User: Сертификат отправлен
        
    else Курс недоступен
        System-->>User: Уведомление о недоступности курса
    end
