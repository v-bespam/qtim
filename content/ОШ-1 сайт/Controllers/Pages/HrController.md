---
date: 2024-09-30
tags:
  - ОШ-1-сайт
---
## HrController

Предоставляет информацию по вакансиям и историям сотрудников

### Endpoints

Контроллер предоставляет следующие эндпоинты:

| Метод | URL                                 | Описание |
| ----- | ----------------------------------- | -------- |
| GET   | `nest/api/hr/common-data/`          |          |
| GET   | `nest/api/hr/main-page-data/`       |          |
| GET   | `nest/api/hr/vacancies/`            |          |
| GET   | `nest/api/hr/vacancy-detail/:id/`   |          |
| GET   | `nest/api/hr/interviews/`           |          |
| GET   | `nest/api/hr/interview-detail/:id/` |          |

### Получить общую информацию для страницы вакансий

`GET nest/api/hr/common-data/`

Получает от Strapi информацию для страницы Вакансии

В случае успеха возвращает 200 Ok

Страница Strapi: HrCommonData, API ID: hr-common-data

### Получить главную страницу вакансий

`GET nest/api/hr/main-page-data/`

Получает от Strapi информацию для страницы Вакансии

В случае успеха возвращает 200 Ok

Страница Strapi: HrMainPage, API ID: hr-main-page

### Получить список вакансий

`GET nest/api/hr/vacancies/`

Получает от Strapi список всех вакансий, отсортированный по возрастанию по полю `Sort`

возвращает 200 Ok

Коллекция Strapi: Vacancies, API ID: vacancy

### Получить подробную информацию о вакансии

`GET nest/api/hr/vacancy-detail/:id/`

Получает от Strapi подробную информацию о вакансии.

id: number - ID вакансии

возвращает 200 Ok

Коллекция Strapi: Vacancies, API ID: vacancy

### Получить истории сотрудников

`GET nest/api/hr/interviews/`

Получает от Strapi истории сотрудников

возвращает 200 Ok

Коллекция Strapi: HrInterviews, API ID: hr-interview

### Получить подробную информацию об истории сотрудника

`GET nest/api/hr/interview-detail/:id/`

id: number - ID вакансии

возвращает 200 Ok

Коллекция Strapi: HrInterviews, API ID: hr-interview