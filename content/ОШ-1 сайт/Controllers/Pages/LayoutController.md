---
date: 2024-09-30
tags:
  - ОШ-1-сайт
---
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
