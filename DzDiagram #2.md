```mermaid
%% Диаграмма компонентов системы управления логистикой и доставкой
component-beta

    %% Основные Компоненты Системы (Backend)
    component [Backend Server] as Backend
    component [Database] as DB
    component [Route Optimization] as RouteOpt
    component [Warehouse Module] as Warehouse
    component [Courier Integration] as CourierAPIModule
    component [Notification System] as NotifSystem
    component [Analytics System] as Analytics

    %% Frontend Компоненты
    component [Web Application (Clients)] as Frontend
    component [Mobile App (Couriers)] as Mobile

    %% Внешние Системы (External Actors)
    component [External Courier Services API] as ExtCourier
    component [Payment Gateway] as PaymentGateway

    %% 1. FRONTEND -> BACKEND (через REST API)
    Frontend --(REST API)--> Backend : Запросы Клиентов
    Mobile --(REST API / WebSockets)--> Backend : Данные Курьеров

    %% 2. BACKEND -> БИЗНЕС-ЛОГИКА
    Backend --> DB : Чтение/Запись данных (SQL)
    Backend --> RouteOpt : Запрос на оптимизацию маршрута (gRPC)
    Backend --> Warehouse : Учет товаров (Inventory API)
    Backend --> CourierAPIModule : Управление доставкой
    Backend --> NotifSystem : Триггер уведомлений
    Backend --> PaymentGateway : Обработка транзакций

    %% 3. ВЗАИМОДЕЙСТВИЕ МОДУЛЕЙ И ВНЕШНИХ СИСТЕМ
    
    %% Интеграция с Курьерами
    CourierAPIModule --(External API)--> ExtCourier : Отправка/Получение статусов
    ExtCourier --(Webhook)--> CourierAPIModule : Обратные вызовы (Статус доставки)

    %% Уведомления
    NotifSystem .-> Frontend : Уведомления Клиентам
    NotifSystem .-> Mobile : Уведомления Курьерам

    %% Аналитика
    Analytics <-. Backend : Сбор данных о доставке
    Analytics --> DB : Чтение данных для отчетов (Report API)

    %% Дополнительно (Функциональные требования)
    note right of Backend
        Высокая доступность
        Безопасность данных
        Поддержка международных поставок
    end

    %% Описание интерфейсов и задач (для полноты)
    note left of Frontend
        Интерфейс: REST API
        Задача: Отображение информации клиентам
    end
    note right of Warehouse
        Интерфейс: Inventory API
        Задача: Учет остатков, резервирование
    end
    note right of CourierAPIModule
        Интерфейс: Courier API
        Задача: Получение статусов, управление курьерами
    end
