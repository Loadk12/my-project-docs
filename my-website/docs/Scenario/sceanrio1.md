---
title: Создание вакансии
sidebar_position: 1
---

# Сценарий создания вакансии

```plantuml

@startuml

actor Recruiter
participant "HR System" as System
participant "Vacancies DB" as DB

== Создание вакансии ==
Recruiter -> System: POST /vacancy (данные + токен)
System -> System: Проверка авторизации
alt Токен валиден
    System -> System: Проверка данных
    alt Данные корректны
        System -> DB: Сохранение вакансии
        DB --> System: Подтверждение
        System --> Recruiter: 201 Created
    else Данные некорректны
        System --> Recruiter: 400 Bad Request
    end
else Токен невалиден
    System --> Recruiter: 401 Unauthorized
end

@enduml
```

## Описание алгоритма

1. **Recruiter** отправляет запрос: `POST /vacancy` с данными вакансии и токеном авторизации.
2. **System** проверяет авторизацию:
   * Если токен валиден:
     * **System** проверяет корректность данных:
       * Если корректны:
         * **System** сохраняет вакансию в **Vacancies DB**.
         * **System** отправляет **Recruiter**: `201 Created`.
       * Если некорректны:
         * **System** отправляет **Recruiter**: `400 Bad Request`.
   * Если токен невалиден:
     * **System** отправляет **Recruiter**: `401 Unauthorized`.
