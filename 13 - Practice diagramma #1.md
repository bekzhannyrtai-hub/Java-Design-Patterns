```mermaid
stateDiagram-v2
    [*] --> Idle
    
    Idle --> CarSelected: selectCar()
    CarSelected --> Idle: cancelOrder()
    CarSelected --> OrderConfirmed: confirmOrder()
    CarSelected --> CarSelected: changeCar()
    
    OrderConfirmed --> CarArrived: carStarted()
    OrderConfirmed --> TripCancelled: cancelOrder()
    
    CarArrived --> InTrip: startTrip()
    CarArrived --> TripCancelled: cancelOrder()
    
    InTrip --> TripCompleted: completeTrip()
    InTrip --> TripCancelled: emergencyCancel()
    
    TripCompleted --> [*]: paymentCompleted()
    TripCompleted --> TripCompleted: paymentFailed()
    
    TripCancelled --> [*]: cleanup()
    
    state CarArrived {
        [*] --> Waiting
        Waiting --> UserNotified: notifyUser()
        UserNotified --> [*]: userResponded()
    }
    
    note right of CarSelected
        Можно изменить автомобиль
        до подтверждения заказа
    end note
    
    note right of TripCompleted
        Возможна система рейтинга
        водителя и поездки
    end note
