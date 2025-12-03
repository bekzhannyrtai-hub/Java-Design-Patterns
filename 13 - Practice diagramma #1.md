```mermaid
stateDiagram-v2
    direction LR

    [*] --> Idle: Начать_Заказ

    state Idle {
        Idle : Ожидание действия
        Idle --> CarSelected: Выбрать_Автомобиль
        Idle --> TripCancelled: Отменить_Заказ
    }

    state CarSelected {
        CarSelected : Автомобиль выбран [cite: 13]
        CarSelected --> OrderConfirmed: Подтвердить_Заказ
        CarSelected --> Idle: Изменить_Автомобиль
        CarSelected --> TripCancelled: Отменить_Заказ
    }

    state OrderConfirmed {
        OrderConfirmed : Автомобиль в пути [cite: 14]
        OrderConfirmed --> CarArrived: Автомобиль_Прибыл
        OrderConfirmed --> OrderConfirmed: Задержка_Автомобиля
        OrderConfirmed --> TripCancelled: Отменить_Заказ
    }

    state CarArrived {
        CarArrived : Автомобиль у клиента [cite: 15]
        CarArrived --> InTrip: Начать_Поездку
        CarArrived --> TripCancelled: Отменить_Заказ
    }

    state InTrip {
        InTrip : Поездка начата [cite: 16]
        InTrip --> TripCompleted: Завершить_Поездку
    }

    state TripCompleted {
        TripCompleted : Ожидание оплаты [cite: 17]
        TripCompleted --> [*]: Оплатить_Заказ / Оплата_Успешна
        TripCompleted --> TripCompleted: Проблема_с_Оплатой
    }
    
    TripCancelled : Заказ отменен [cite: 18]
    TripCancelled --> [*]: Ожидание_Нового_Заказа
