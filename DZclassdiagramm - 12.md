```mermaid
activityDiagram
  title Процесс найма сотрудников
  start
  
  partition Руководитель отдела {
    :Создать заявку на вакансию;
    --> ЗаявкаСоздана
  }
  
  partition HR-отдел {
    ЗаявкаСоздана --> :Проверить заявку;
    --> Имеется соответствие требованиям?
    
    if (соответствует) then (Да)
      :Утвердить заявку;
      --> VacancyApproved
    else (Нет)
      :Уведомить о необходимости доработки;
      --> ДоработкаЗаявки
    end
  }
  
  partition Руководитель отдела {
    ДоработкаЗаявки --> :Доработать заявку;
    --> ЗаявкаСоздана
  }

  VacancyApproved --> fork NameFork1

  NameFork1 --> Публикация
  NameFork1 --> ПриемЗаявок

  partition Система {
    Публикация: Опубликовать вакансию на сайте;
    --> VacancyPublished
  }

  partition Кандидат {
    ПриемЗаявок: Подавать заявки;
    --> ApplicationsReceived
  }

  VacancyPublished --> join NameFork1
  ApplicationsReceived --> join NameFork1
  
  join NameFork1 --> ПроверкаАнкет

  partition HR-отдел {
    ПроверкаАнкет: Проверить анкеты кандидатов;
    --> Кандидат подходит?
    
    if (подходит) then (Да)
      :Пригласить на первичное собеседование;
      --> InterviewStart
    else (Нет)
      :Отклонить анкету;
      --> Отказ1
    end
  }
  
  partition Кандидат {
    Отказ1: Получить уведомление об отказе;
    --> end
  }

  InterviewStart --> partition HR-менеджер {
    :Провести первичное интервью;
    --> ПервичноеПроверено
  }

  ПервичноеПроверено --> partition Руководитель отдела {
    :Провести техническое собеседование;
    --> ТехническоеПроверено
  }

  ТехническоеПроверено --> :Собеседования успешно пройдены?;

  if (успешно) then (Да)
    :Предложить оффер;
    --> OfferSent
  else (Нет)
    partition HR-менеджер {
      :Уведомить кандидата об отказе;
      --> end
    }
  end

  OfferSent --> partition Кандидат {
    :Подтвердить оффер;
    --> OfferConfirmed
  }

  OfferConfirmed --> fork NameFork2

  NameFork2 --> ITNotification
  NameFork2 --> EmployeeAddition

  partition HR-отдел {
    ITNotification: Уведомить IT-отдел о необходимости настройки рабочего места;
    --> ITNotified
  }

  partition Система {
    EmployeeAddition: Добавить нового сотрудника в базу данных;
    --> EmployeeAdded
  }

  ITNotified --> join NameFork2
  EmployeeAdded --> join NameFork2
  
  join NameFork2 --> end
