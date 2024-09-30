---
date: 2024-09-30
tags:
  - ОШ-1-сайт
---
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

Получает информацию для страницы Новости и разделы новостей, хлебные крошки

возвращает 200 Ok

Страница Strapi: NewsPageInfo, API ID: news-page-info
Коллекция Strapi: NewsSections, API ID: news-section

```json
breadcrumbs = [
 {
  title: 'Главная',
  url: '/',
 },
 {
  title: 'Новости',
  url: '/news/',
 },
];
```

### Получить список всех новостей

`GET nest/api/news/all`

Получает список всех новостей на сайте

В query может быть передан section?: string; - код секции
limit: number; - опциональный
offset: number; - опциональный

offset по умолчанию равен 0, а limit — 11

возвращает 200 Ok

массив новостей из кэша Redis по ключу `news`
Коллекция Strapi: SchoolNews, API ID: school-news, сортировка в порядке уменьшения

`hasMoreNews` равен `true` если есть еще новости в списке

```json
{
hasMoreNews: boolean;
news: News[]
}
```

News:

```json
{
  authorName: string | null;
  code: string;
  id: number;
  published_at: Date;
  section: NewsSection;
  text: string;
  title: string;
  meta?: Meta;
  img?: Image;
}
```

### Получить подробную информацию о новости

`GET nest/api/news/detail/:code`

code: string - код новости

Получить 
В случае если новость с указанным кодом не найдена, выбрасывает исключение с текстом 'News not found'

К хлебным крошкам добавляется текущий заголовок новости

новость из кэша Redis по ключу `news:${code}`
Коллекция Strapi: SchoolNews, API ID: school-news
Страница Strapi: NewsPageInfo, API ID : news-page-info, блоки SocialLinks, WelcomeBlock, Form