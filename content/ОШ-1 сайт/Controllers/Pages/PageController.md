---
date: 2024-09-30
tags:
  - ОШ-1-сайт
---
## PageController

Отвечает за получение информации о странице

### Endpoints

Контроллер предоставляет следующие эндпоинты:

| Метод | URL                               | Описание                         |
| ----- | --------------------------------- | -------------------------------- |
| GET   | `nest/api/pages/`                 | Получить информацию для страницы |
| GET   | `nest/api/pages/karta-sayta/`     |                                  |
| GET   | `nest/api/pages/sitemap/`         |                                  |
| GET   | `nest/api/pages/cosmos-data/`     |                                  |
| GET   | `nest/api/pages/biblioteka-data/` |                                  |
| POST  | `nest/api/pages/deactivate/`      |                                  |

### Получить информацию о странице

`GET nest/api/pages/`

В query должен быть передан url страницы - code: string

Вообще не понятно как работает

В случае если страницы с указанным кодом не найдена, выбрасывает исключение с текстом 'Page not found'

из кэша Redis по ключу `page:${pageCode}`
Коллекция Strapi: Pages, API ID: page

**Выходные данные:** PageDto 200 Ok

```json
{
  id: number;
  url: string;
  published_at: string | null;
  created_at: string;
  updated_at: string;
  blocks: ConstructorBlock[];
  headerMenuItems: HeaderAnchorMenuItem[];
  meta: Meta;
  breadcrumbs: BreadcrumbItem[];
  contactUsSocialLinks: SocialLinks[];
  sitemapConfig: SitemapConfig | null;
}
```

### Карта сайта

`GET nest/api/pages/karta-sayta/`

Составление карты сайта

Пытается получить данные в кэше Redis по ключу `pages-for-${type}` karta-sayta
Если не найдено, обращается к Strapi, получает все страницы коллекции Pages, сортировка по url по увеличению, получает отдельные страницы Strapi. Все объединяется в массив, из которого исключаются страницы с мета тегами `excludeFromSitemap` и `canonical`.

Заголовок страницы (`title`) формируется на основе мета-данных `sitemapTitle` или содержимого блока `banner-block`.

Выходные данные: 200 Ok

Возвращает объекты страниц карты сайта

```json
{
  id: page.id,
  url: page.url,
  title,
  updatedAt: page.updated_at,
  sitemapConfig: page.sitemapConfig,
};
```

### Sitemap

`GET nest/api/pages/sitemap/`

Аналогичен [[#Карта сайта|Карта сайта]], но выполняется поиск по ключу `pages-for-${type}` sitemap# Мобильное приложение «Онлайн‑школа.  
Наука в AR»

### Получение страницы Мобильного приложения «Онлайн‑школа. Наука в AR»

`GET nest/api/pages/cosmos-data/`

Получение данных страницы Мобильного приложения «Онлайн‑школа. Наука в AR». Поиск в Redis по ключу `cosmos-data`. Страница в Strapi: Cosmos, API ID: cosmos

Выходные данные: + данные из Strapi 200 Ok

```json
{
  header: string;
  whatIsText: string;
  functionsHeader: string;
  functions?: ImgWithTitleAndText[];
  interestingHeader: string;
  interestingItems?: ImgWithTitleAndText[];
  bottomHeader: string;
  appStoreLink: string;
  googlePlayLink: string;
  meta?: Meta;
}
```

ImgWithTitleAndText:

```json
{
  title: string;
  text: string;
}
```

Meta:

```json
{
  pageName?: string;
  title?: string;
  description?: string;
  canonical?: string;
  isFaqPage?: boolean;
  excludeFromSitemap?: boolean;
  breadcrumbTitle?: string;
  sitemapTitle?: string;
}
```

### Получение страницы мобильного приложения Цифровая библиотека

`GET nest/api/pages/biblioteka-data/`

Получение страницы мобильного приложения Цифровая библиотека. Поиск в Redis по ключу `biblioteka-data`. Страница в Strapi: Biblioteka, API ID: biblioteka

Выходные данные: + данные из Strapi 200 Ok

```json
{
  header: string;
  aboutText: string;
  functionsHeader: string;
  functions?: ImgWithTitleAndText[];
  interestingHeader: string;
  interestingItems?: ImgWithTitleAndText[];
  bottomHeader: string;
  appStoreLink: string;
  googlePlayLink: string;
  meta?: Meta;
}
```

ImgWithTitleAndText:

```json
{
  title: string;
  text: string;
}
```

Meta:

```json
{
  pageName?: string;
  title?: string;
  description?: string;
  canonical?: string;
  isFaqPage?: boolean;
  excludeFromSitemap?: boolean;
  breadcrumbTitle?: string;
  sitemapTitle?: string;
}
```

### Переместить страницу в черновик

`POST nest/api/pages/deactivate/`

В тело запроса должны быть переданы: redirectUrls: string[];

Получает массив строк с URL страниц, находит их в Strapi, устанавливает для поля published_at значение null.

200 Ok