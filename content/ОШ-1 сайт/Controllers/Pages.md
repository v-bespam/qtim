---
date: 2024-09-26
tags:
  - qtim
---
Предназначен для получения информации, содержащейся на страницах сайта.

Состоит из следующих контроллеров:

1. CoursesController
2. FaqController
3. FormsController
4. HrController
5. LandingController
6. LayoutController
7. NewsController
8. PageController
9. TutorsController

## CoursesController

Контроллер предназначен для получения информации о курса и отзывах

### Endpoints

Контроллер предоставляет следующие эндпоинты:

| Метод | URL                                   | Описание                                                                            |
| ----- | ------------------------------------- | ----------------------------------------------------------------------------------- |
| GET   | `nest/api/courses/`                   | [[#Получение списка курсов\|Получение списка курсов]]                               |
| GET   | `nest/api/courses/detail/:code`       | [[#Получение подробной информации о курсе\|Получение подробной информации о курсе]] |
| GET   | `nest/api/courses/review-answers/:id` | [[Pages#Получение отзыва]]                                                          |
| POST  | `nest/api/courses/review-like`        | [[Pages#Поставить лайк на отзыв]]                                                   |


### Получение списка курсов

`GET nest/api/courses/`

В query параметрах могут быть заданы значения фильтров (loadFilters) `loadFilters?: boolean` Возвращать ли возможные фильтры для курсов

отвечает за получение информации о странице курсов.

Возвращает информацию о странице с курсами, включая хлебные крошки, а также массив объектов с информацией о курсах

Страница в Strapi: CoursesPageInfo, API ID: courses-page-info
Для фильтров, коллекция в Strapi: CourseFilterValues

### Получение подробной информации о курсе

`GEY nest/api/courses/detail/:code`

В запросе должен быть передан код курса
В query параметрах могут быть заданы значения фильтров (loadFilters) `loadFilters?: boolean`

возвращает подробную информацию о конкретном курсе

Возвращает объект с подробной информацией о курсе
Коллекция в Strapi: Courses

### Получение отзыва

`GET nest/api/courses/review-answers/:id`

Получить информацию по отзыву на курс по его ID

В запросе должен быть передан код отзыва
Коллекция в Strapi: CourseReviews

### Поставить лайк на отзыв

`POST nest/api/courses/review-like`

В body должны быть переданы параметры

reviewId: number
likesCount: number

Выполняет 

При помощи RequestPayload получает хэш пользователя и проверят ставил ли он уже лайк на этот отзыв. В случае, если пользователь еще не ставил лайк, передайет Strapi новое количество лайков
Коллекция в Strapi: CourseReviews

## FaqController

Контроллер предназначен для получения страниц раздела вопросы и ответы

### Endpoints

Контроллер предоставляет следующие эндпоинты:

| Метод | URL             | Описание                                      |
| ----- | --------------- | --------------------------------------------- |
| GET   | `nest/api/faq/` | [[Pages#Получение страницы вопросы и ответы]] |

### Получение страницы вопросы и ответы

`GET nest/api/faq/`

В query параметрах может быть передан код страницы раздела вопросы и ответы `code: string`

Заправшивает
страницу Strapi: FAQCommonData API ID: faq-common-data
коллекцию Strapi: FAQGroups

Возвращает объект с информацией о странице и хлебных крошках

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

## LandingController

Отвечает за получение информации для лэндинга "Учебна на выживание" - https://onlineschool-1.ru/schoollife/

### Endpoints

Контроллер предоставляет следующие эндпоинты:

| Метод | URL                 | Описание                         |
| ----- | ------------------- | -------------------------------- |
| GET   | `nest/api/landing/` | Получить информацию для страницы |

### Получить информацию для страницы

`GET nest/api/landing/`

Получает от Strapi все элементы страницы ScoolLifeBalance

возвращает 200 Ok

Страница Strapi: ScoolLifeBalance, API ID: scool-life-balance

## LayoutController

Получить разметку страницы

`GET nest/api/layout/`

В один объект Получает из Strapi страницы:

- AsideMenu, API ID: aside-menu
- NewAsideMenu, API ID: new-aside-menu
- FooterInfo, API ID: footer-info
- NewFooterInfo, API ID: new-footer-info

Коллекцию RegionContacts, API ID: region-contact. Сортировка по возрастаю, по полю `Sort`

возвращает 200 Ok

```json
menu: [],
newMenu: [],
footerInfo: [],
newFooterInfo: [],
regionContacts: [],
```

## NewsController

Отвечает за получение информации о новостях

### Endpoints

Контроллер предоставляет следующие эндпоинты:

| Метод | URL                          | Описание |
| ----- | ---------------------------- | -------- |
| GET   | `nest/api/news/`             |          |
| GET   | `nest/api/news/all`          |          |
| GET   | `nest/api/news/detail/:code` |          |

### Получить информацию для страницы новостей

`GET nest/api/news/`

Получает от Strapi информацию для страницы Новости и разделы новостей, хлебные крошки

возвращает 200 Ok

Страница Strapi: NewsPageInfo, API ID: news-page-info
Коллекция Strapi: NewsSections, API ID: news-section