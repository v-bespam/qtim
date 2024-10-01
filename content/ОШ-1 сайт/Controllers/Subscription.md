---
date: 2024-09-30
tags:
  - ОШ-1-сайт
---
Предназначен для формирования списков рассылки.

## SubscriptionController

Позволяет выполнять запросы к API Unisender для сохранения адреса электронной почты в списке рассылки.

### Endpoints

Контроллер предоставляет следующий эндпоинт:

| Метод | URL                            | Описание                                        |
| ----- | ------------------------------ | ----------------------------------------------- |
| POST  | `nest/api/subscription/email/` | [[#Подписка на рассылку\|Подписка на рассылку]] |

### Подписка на рассылку

`POST nest/api/subscription/email/`

В тело запроса должен быть передан параметр email: string;

Отправляет GET запрос к API Unisender https://api.unisender.com/ru/api/subscribe, аодержащий следующую информацию:

```json
{
  format: 'json',
  api_key: process.env.UNISENDER_API_KEY,
  list_ids: '1',
  double_optin: 3,
  'fields[email]': dto.email,
};
```

Если при выполнении запроса возникает ошибка выбрасывается исключение BadRequestException с сообщением об ошибке.