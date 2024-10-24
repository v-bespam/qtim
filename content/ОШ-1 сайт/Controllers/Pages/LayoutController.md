---
date: 2024-09-30
tags:
  - ОШ-1-сайт
---
Контроллер предназначен для получения разметки страницы

### Endpoints

Контроллер предоставляет следующий эндпоинт:

| Метод | URL                | Описание                                                      |
| ----- | ------------------ | ------------------------------------------------------------- |
| GET   | `nest/api/layout/` | [[#Получение разметки страницы\|Получение разметки страницы]] |

### Получение разметки страницы

`GET nest/api/layout/`

*Входные данные:* отсутствуют

*Функционал:*

Объединяет в один объект данные страниц Strapi:

- **menu** - выполняет поиск в кэше Redis по ключу `layout-menu`, если данные не найдены, получает в Strapi элементы страницы AsideMenu (API ID: aside-menu). Сохраняет их в кэш.
- **newMenu** - выполняет поиск в кэше Redis по ключу `new-layout-menu`, если данные не найдены, получает в Strapi элементы страницы NewAsideMenu (API ID: new-aside-menu). Сохраняет их в кэш.
- **footerInfo** - выполняет поиск в кэше Redis по ключу `footer-info`, если данные не найдены, получает в Strapi элементы страницы FooterInfo (API ID: footer-info). Сохраняет их в кэш.
- **newFooterInfo** - выполняет поиск в кэше Redis по ключу `new-footer-info`, если данные не найдены, получает в Strapi элементы страницы NewFooterInfo (API ID: new-footer-info). Сохраняет их в кэш.
- **regionContacts** - выполняет поиск в кэше Redis по ключу `region-contacts`, если данные не найдены, получает в Strapi элементы коллекции RegionContacts (API ID: region-contact), отсортированные по возрастанию. Генерирует URL, добавляя к нему поле `canonical` из свойства `meta`, если оно отсутствует, то URL генерируется из `page.url`. Сохраняет данные в кэш.

*Выходные данные:* Status: `200 OK`

Возвращает объект с массивами данных для разметки из Strapi.

```json
menu: [],
newMenu: [],
footerInfo: [],
newFooterInfo: [],
regionContacts: [],
```
