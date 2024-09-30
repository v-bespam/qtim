---
date: 2024-09-30
tags:
  - qtim
---
## FormsController

Определяет работу с формами на сайте

### Endpoints

Контроллер предоставляет следующие эндпоинты:

| Метод | URL                                    | Описание                                                |
| ----- | -------------------------------------- | ------------------------------------------------------- |
| POST  | `nest/api/forms/request/`              | [[#Оставить заявку на сайте\|Оставить заявку на сайте]] |
| POST  | `nest/api/forms/remark/`               |                                                         |
| POST  | `nest/api/forms/buy/`                  |                                                         |
| POST  | `nest/api/forms/course-review/`        |                                                         |
| POST  | `nest/api/forms/respond-to-vacancy/`   |                                                         |
| POST  | `nest/api/forms/recommend-to-vacancy/` |                                                         |

### Оставить заявку на сайте

`POST nest/api/forms/request/`

Позволяет отправить информацию о заполненной форме на сайте. оставить **заявку**.

В тело запроса должны быть переданы параметры

- leadName?: string;
- name: string;
- phone: string;
- email?: string;
- company?: string;
- question?: string;
- referer: string; - ссылка на страницу, с которой был оставлена заявка

Отправляет в Strapi данные заполненной формы сайта

Коллекция Strapi: FormRequests, API ID: form-request

В случае успеха возвращает 201 Created

### Отправить данные формы

`POST nest/api/forms/remark/`

Позволяет отправить информацию о заполненной форме связи на сайте.

В тело запроса должны быть переданы параметры

- name: string;
- phone: string;
- email: string;
- text: string; - текст сообщения

Отправляет в Strapi данные заполненной формы сайта

Коллекция Strapi: FormRemarks, API ID: form-remarks

В случае успеха возвращает 201 Created

### Отправить заявку записи на курс

`POST nest/api/forms/buy/`

Позволяет отправить заявку записи на курс

В тело запроса должны быть переданы параметры

- leadName?: string;
- name: string;
- phone: string;
- email?: string;
- company?: string;
- question?: string;
- course: number; - id курса

Отправляет в Strapi данные заполненной формы сайта

Коллекция Strapi: BuyRequests, API ID: buy-request

В случае успеха возвращает 201 Created
### Оставить отзыв на курс

`POST nest/api/forms/course-review/`

Отправляет в Strapi отзыв на курс

проверяет fingerprint пользователя, может ли он оставить отзыв
В запросе может быть передано изображение. Максимальный объем 10 Мб
В тело запроса должны быть переданы параметры:

- name: string;
- text: string;
- starsCount: number;
- course_review?: number;
- course?: number;


В случае успеха возвращает 201 Created

Коллекция Strapi: CourseReviews, API ID: course-review

### Откликнуться на вакансию

`POST nest/api/forms/respond-to-vacancy/`

Отправляет в Strapi отклик на вакансию

В запросе может быть передано изображение. Максимальный объем 10 Мб
В тело запроса должны быть переданы параметры:

- name: string;
- surname: string;
- phone: string;
- email: string;
- vacancy?: number;
- subject?: number;
- resumeLink?: string;
- aboutMe?: string;

В случае успеха возвращает 201 Created

Коллекция Strapi: VacancyRequests, API ID: vacancy-request

### Рекомендация на вакансию

`POST nest/api/forms/recommend-to-vacancy/`

Отправляет в Strapi рекомендацию на вакансию

В запросе может быть передано изображение. Максимальный объем 10 Мб
В тело запроса должны быть переданы параметры:

- name: string;
- surname: string;
- phone: string;
- vacancy: number; - должность
- resumeLink?: string;
- sourceUserName: string; - кто отправил
- sourceUserSurname: string;
- sourceUserEmail: string;
- sourceUserPhone: string;
- sourceUserIsEmployee: string;

В случае успеха возвращает 201 Created

Коллекция Strapi: HrRecommendFormRequests, API ID: hr-recommend-form-request