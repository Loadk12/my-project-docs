---
title: ERD
sidebar_position: 1
---

# Модель данных

import Drawio from '@theme/Drawio'
import diagram from '!!raw-loader!./model.drawio';

<Drawio content={diagram} editable={false} />


## Users

| Название          | Тип          | Описание                               |
| ----------------- | ------------ | -------------------------------------- |
| ID                | NUMBER(14,0) | Идентификатор пользователя (PK)        |
| Name              | VARCHAR(50)  | Имя пользователя                       |
| Email             | VARCHAR(100) | Email (уникальный, NOT NULL)           |
| Profile           | TEXT         | Профиль (навыки, опыт)                 |
| Registration_Date | DATE         | Дата регистрации                       |
| Status            | VARCHAR(50)  | Статус пользователя                    |

## Recommendations

| Название            | Тип          | Описание                                      |
| ------------------- | ------------ | --------------------------------------------- |
| ID                  | NUMBER(14,0) | Идентификатор рекомендации (PK)               |
| User_id             | NUMBER(14,0) | Идентификатор пользователя (FK → Users)       |
| Recommendation_Type | ENUM         | Тип рекомендации (vacancy, course, career-path)|
| Object_id           | NUMBER(14,0) | Идентификатор объекта (FK на ресурс)          |
| Creation_Time       | DATE         | Дата создания рекомендации                    |
| Status              | ENUM         | Статус рекомендации                           |

## Courses

| Название         | Тип          | Описание                        |
| ---------------- | ------------ | --------------------------------|
| ID               | NUMBER(14,0) | Идентификатор курса (PK)        |
| Course_Name      | VARCHAR(100) | Название курса (NOT NULL)       |
| Description      | TEXT         | Описание курса                  |
| Platform         | VARCHAR(50)  | Платформа курса                 |
| Link             | VARCHAR(200) | Ссылка на курс                  |
| Start_Date       | DATE         | Дата начала курса               |
| End_Date         | DATE         | Дата окончания курса            |
| Difficulty_Level | ENUM         | Уровень сложности курса         |

## Vacancies_and_Internships

| Название            | Тип                        | Описание                                |
| ------------------- | -------------------------- | --------------------------------------- |
| ID                  | NUMBER(14,0)               | Идентификатор (PK)                      |
| Title               | VARCHAR(100)               | Название вакансии/стажировки (NOT NULL) |
| Type                | ENUM('Vacancy','Internship')| Тип (Vacancy/Internship), NOT NULL      |
| Description         | TEXT                       | Описание вакансии/стажировки            |
| Requirements        | TEXT                       | Требования к кандидату                  |
| Company             | VARCHAR(100)               | Компания                                |
| Salary              | DECIMAL(10,2)              | Зарплата                                |
| Application_Deadline| DATE                       | Крайний срок подачи заявки              |
| Link                | VARCHAR(200)               | Ссылка на подробную информацию          |

## Skills

| Название      | Тип          | Описание                   |
| ------------- | ------------ | -------------------------- |
| ID            | NUMBER(14,0) | Идентификатор навыка (PK)  |
| Skill_name    | VARCHAR(70)  | Название навыка            |
| Description_s | TEXT         | Описание навыка            |

## Users_Skills

| Название | Тип          | Описание                                   |
| -------- | ------------ | ------------------------------------------ |
| User_id  | NUMBER(14,0) | Идентификатор пользователя (FK → Users)    |
| Skill_id | NUMBER(14,0) | Идентификатор навыка (FK → Skills)         |

## Vacancies_Skills

| Название   | Тип          | Описание                                 |
| ---------- | ------------ | ---------------------------------------- |
| Vacancy_id | NUMBER(14,0) | Идентификатор вакансии (FK → Vacancies)  |
| Skill_id   | NUMBER(14,0) | Идентификатор навыка (FK → Skills)       |

## Courses_Skills

| Название  | Тип          | Описание                             |
| --------- | ------------ | ------------------------------------ |
| Course_id | NUMBER(14,0) | Идентификатор курса (FK → Courses)   |
| Skill_id  | NUMBER(14,0) | Идентификатор навыка (FK → Skills)   |
