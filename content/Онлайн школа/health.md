---
date: 2024-10-02
tags:
  - "#Онлайн-школа"
---
Модуль предназначен для проверки состояния соединения с базой данных при помощи модуля @nestjs/terminus, а также для проверки работоспособности приложения в целом.

## HealthController

### Endpoints

Контроллер предоставляет следующие эндпоинты:

| Метод | URL             | Описание                                                                          |
| ----- | --------------- | --------------------------------------------------------------------------------- |
| GET   | `health/ready/` | [[#Проверка доступности базы данных\|Проверка доступности базы данных]]           |
| GET   | `health/alive/` | [[#Проверка работоспособности приложения\|Проверка работоспособности приложения]] |

### Проверка доступности базы данных

`GET health/ready`

*Входные данные:* Отсутствуют

*Функционал:*

После отправки GET запроса по указанному URL, TypeOrm health indicator выполняет проверку работоспособности базы данных, выполняя простую SQL команду `SELECT 1`. Время ожидания ответа - 5 секунд.

*Выходные данные:*

```json
{
  status: 'error' | 'ok' | 'shutting_down'
  info?: {
    db: {
      status: up
    }
  }
  error?: {
    db: {
      status: down
    }
  }
  details: {
    db: {
      status: up | down
    }
  }
}
```

### Проверка работоспособности приложения

`GET health/alive`

*Входные данные:* Отсутствуют

*Функционал:*

Выполняет простую проверку доступности приложения: в случае нормальной работы возвращает на запрос ответ true с кодом `200 OK`.

*Выходные данные:* Status: `200 OK`