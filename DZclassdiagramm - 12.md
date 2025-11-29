```mermaid
activityDiagram
    
    start
    
    partition Руководитель отдела {
      :Создать заявку на вакансию;
      --> Заявка;
    }
    
    partition HR-отдел {
      :Проверить заявку;
      --> Имеется соответствие требованиям?;
      
      if (соответствует) then (Да)
        :Утвердить заявку;
        --> VacancyApproved;
      else (Нет)
        :Уведомить о необходимости доработки;
        --> Доработка;
      end
    }
    
    partition Руководитель отдела {
      Доработка:Доработать заявку;
      --> Заявка;
    }

    VacancydApproved --> Fork;

    Fork: Fork
    Fork --> Публикация;
    Fork --> ПодачаЗаявок;

    partition Система {
      Публикация:Опубликовать вакансию на сайте;
      --> VacancyPublished;
    }

    partition Кандидат {
      ПодачаЗаявок:Подавать заявки;
      --> ApplicationsReceived;
    }

    VacancyPublished --> Join1;
    ApplicationsReceived --> Join1;
    Join1: Join

    Join1 --> partition HR-отдел {
      :Проверить анкеты кандидатов;
      --> Кандидат подходит?;

      if (подходит) then (Да)
        :Пригласить на первичное собеседование;
        --> InterviewStart;
      else (Нет)
        :Отклонить анкету;
        --> Отказ1;
      end
    }
    
    partition Кандидат {
        Отказ1:Получить уведомление об отказе;
        --> end
    }

    InterviewStart --> partition HR-менеджер {
      :Провести первичное интервью;
      --> ПервичноеПроверено;
    }

    ПервичноеПроверено --> partition Руководитель отдела {
      :Провести техническое собеседование;
      --> ТехническоеПроверено;
    }

    ТехническоеПроверено --> :Собеседования успешно пройдены?;

    if (успешно) then (Да)
      :Предложить оффер;
      --> OfferSent;
    else (Нет)
      partition HR-менеджер {
        :Уведомить кандидата об отказе;
        --> end
      }
    end

    OfferSent --> partition Кандидат {
      :Подтвердить оффер;
      --> OfferConfirmed;
    }

    OfferConfirmed --> ForkFinal;

    ForkFinal: Fork
    ForkFinal --> ITNotification;
    ForkFinal --> EmployeeAddition;
    
    partition HR-отдел {
      ITNotification:Уведомить IT-отдел о необходимости настройки рабочего места;
      --> ITNotified;
    }

    partition Система {
      EmployeeAddition:Добавить нового сотрудника в базу данных;
      --> EmployeeAdded;
    }

    ITNotified --> JoinFinal;
    EmployeeAdded --> JoinFinal;
    JoinFinal: Join

    JoinFinal --> end
