---
date: 2024-09-30
tags:
  - ОШ-1-сайт
---
Контроллер предназначен для получения информации о курсах и отзывах о них.

### Endpoints

Контроллер предоставляет следующие эндпоинты:

| Метод | URL                                   | Описание                                                                                  |
| ----- | ------------------------------------- | ----------------------------------------------------------------------------------------- |
| GET   | `nest/api/courses/`                   | [[#Получение страницы с информацией о курсах\|Получение страницы с информацией о курсах]] |
| GET   | `nest/api/courses/detail/:code`       | [[#Получение подробной информации о курсе\|Получение подробной информации о курсе]]       |
| GET   | `nest/api/courses/review-answers/:id` | [[#Получение отзыва\|Получение отзыва]]                                                   |
| POST  | `nest/api/courses/review-like`        | [[#Обновить количество лайков отзыва\|Обновить количество лайков отзыва]]                 |

### Получение страницы с информацией о курсах

`GET nest/api/courses/`

*Входные данные:*

- Query параметры:

| Параметр    | Тип данных | Валидация    | Описание                                   |
| ----------- | ---------- | ------------ | ------------------------------------------ |
| loadFilters | boolean    | Опциональный | Возвращать ли возможные фильтры для курсов |

*Функционал:*

Выполняет поиск в кэше Redis по ключу `courses-page-info`, если данные не найдены, подготавливает их: выполняет запрос к Strapi для получения страницы CoursesPageInfo (API ID: courses-page-info). Затем получает список курсов из коллекции Courses в Strapi (API ID: course), добавляет к каждому элементу `buyForm` со страницы CoursesPageInfo, если они не указаны. Формирует хлебные крошки, записывает данные в Redis и возвращает их.

Если параметр задан параметр loadFilters выполняет поиск в Redis по ключу `course-filter-values`, при отсутствии обращается к Strapi для получения коллекции CourseFilterValues (API ID: course-filter-value), сохраняет в кэш и добавляет поле к возвращаемым данным.

*Выходные данные:* Status: `200 OK`

Возвращает объект с данными страницы CoursesPageInfo, список курсов коллекции Courses, хлебные крошки и при необходимости фильтры CourseFilterValues из Strapi.

### Получение подробной информации о курсе

`GET nest/api/courses/detail/:code`

*Входные данные:*

- В запросе должен быть передан код курса - `code: string`
- Query параметры:

| Параметр    | Тип данных | Валидация    | Описание                                   |
| ----------- | ---------- | ------------ | ------------------------------------------ |
| loadFilters | boolean    | Опциональный | Возвращать ли возможные фильтры для курсов |

*Функционал:*

Выполняет поиск в кэше Redis по ключу `course:${code}`, если данные не найдены, подготавливает их:

1. выполняет запрос к Strapi для получения информации о конкретном курсе из коллекции Courses (API ID: course)
2. запрашивает общую информацию о странице и `buyForm` аналогично [[#Получение страницы с информацией о курсах]]
3. Формирует хлебные крошки

Записывает подготовленные данные в Redis и возвращает их.

Если параметр задан параметр loadFilters выполняет поиск в Redis по ключу `course-filter-values`, при отсутствии обращается к Strapi для получения коллекции CourseFilterValues (API ID: course-filter-value), сохраняет в кэш и добавляет поле к возвращаемым данным.

Если курс с указанным кодом не найден, выбрасывает исключение NotFoundException с сообщением об ошибке: Course not found

*Выходные данные:* Status: `200 OK`

Возвращает объект с подробной информацией о курсе из коллекции Courses, общую информацию о странице курсов CoursesPageInfo, хлебные крошки и при необходимости фильтры CourseFilterValues в Strapi

### Получение отзыва

`GET nest/api/courses/review-answers/:id`

*Входные данные:*

- В запросе должен быть передан id отзыва - `id: number`

*Функционал:*

Выполняет поиск в кэше Redis по ключу `course-review-answers:${reviewId}`, если данные не найдены, выполняет запрос к Strapi для поиска в коллекции CourseReviews (API ID: course-review) отзыва с указанным ID. Сохраняет данные в Redis и возвращает их.

*Выходные данные:* Status: `200 OK`

Возвращает объект с информацией об отзыве на курс из коллекции Strapi CourseReviews, в соответствии с переданным запросом.

### Обновить количество лайков отзыва

`POST nest/api/courses/review-like`

*Входные данные:*

- В тело запроса должны быть переданы следующие параметры:

| Параметр   | Тип данных | Валидация    | Описание          |
| ---------- | ---------- | ------------ | ----------------- |
| reviewId   | number     | Обязательный | ID отзыва         |
| likesCount | number     | Обязательный | Количество лайков |

*Функционал:*

При помощи RequestPayload получает `fingerprint.hash` пользователя и сверяет ставил ли он уже лайк на этот отзыв. В случае, если пользователь не ставил лайк, передает Strapi запрос на обновление количества лайков `likesCount` указанного отзыва в коллекции CourseReviews (API ID: course-review).

*Выходные данные:* Status: `200 OK`
