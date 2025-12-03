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
        CarSelected : Автомобиль выбран
        CarSelected --> OrderConfirmed: Подтвердить_Заказ
        CarSelected --> Idle: Изменить_Автомобиль
        CarSelected --> TripCancelled: Отменить_Заказ
    }

    state OrderConfirmed {
        OrderConfirmed : Автомобиль в пути
        OrderConfirmed --> CarArrived: Автомобиль_Прибыл
        OrderConfirmed --> OrderConfirmed: Задержка_Автомобиля
        OrderConfirmed --> TripCancelled: Отменить_Заказ
    }

    state CarArrived {
        CarArrived : Автомобиль у клиента
        CarArrived --> InTrip: Начать_Поездку
        CarArrived --> TripCancelled: Отменить_Заказ
    }

    state InTrip {
        InTrip : Поездка
        InTrip --> TripCompleted: Завершить_Поездку
    }

    state TripCompleted {
        TripCompleted : Ожидание оплаты
        TripCompleted --> [*]: Оплатить_Заказ / Оплата_Успешна
        TripCompleted --> TripCompleted: Проблема_с_Оплатой
    }
    
    TripCancelled : Заказ отменен
    TripCancelled --> [*]: Ожидание_Нового_Заказа
