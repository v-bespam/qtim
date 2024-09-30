---
date: 2024-09-30
tags:
  - qtim
---
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