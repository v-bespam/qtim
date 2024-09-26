---
date: 2024-09-26
tags:
  - qtim
---
Предназначен

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

Контроллер предназначен для

### Endpoints

Контроллер предоставляет следующие эндпоинты:

| Метод | URL                                   | Описание                                    |
| ----- | ------------------------------------- | ------------------------------------------- |
| GET   | `nest/api/courses/`                   | [[#Получение списка курсов]]                |
| GET   | `nest/api/courses/detail/:code`       | [[#Получение подробной информации о курсе]] |
| GET   | `nest/api/courses/review-answers/:id` |                                             |
| POST  | `nest/api/courses/review-like`        |                                             |

### Получение списка курсов

`GET nest/api/courses/`

В query параметрах могут быть заданы значения фильтров (loadFilters) `loadFilters?: boolean` Возвращать ли возможные фильтры для курсов

отвечает за получение информации о странице курсов. Фильтрует результаты в соответствии с query запросом

Возвращает информацию о странице с курсами, включая хлебные крошки, а также массив объектов с информацией о курсах

### Получение подробной информации о курсе

`GEY nest/api/courses/detail/:code`

В запросе должен быть передан код курса
В query параметрах могут быть заданы значения фильтров (loadFilters) `loadFilters?: boolean`

возвращает подробную информацию о конкретном курсе

Возвращает объект с подробной информацией о курсе

###
