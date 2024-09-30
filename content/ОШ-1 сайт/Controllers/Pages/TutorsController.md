---
date: 2024-09-30
tags:
  - ОШ-1-сайт
---
## TutorsController

Отвечает за получение информации о

### Endpoints

Контроллер предоставляет следующие эндпоинты:

| Метод | URL                            | Описание |
| ----- | ------------------------------ | -------- |
| GET   | `nest/api/tutors/`             |          |
| GET   | `nest/api/tutors/all/`         |          |
| GET   | `nest/api/tutors/study/all/`   |          |
| GET   | `nest/api/tutors/detail/:code` |          |

### Страница преподавателей

`GET nest/api/tutors/`

Получает получить информацию для страницы об учителях и преподавателях

Выполняет поиск в кэше redis по ключу tutors-page-info, запрашивает в Strapi страницу TutorsPageInfo, API ID: tutors-page-info. Добавляет информацию о хлебных крошках Главная/Преподаватели и блок free-week-data-block

Возвращает подготовленные данные 200 Ok

### Получить список преподавателей

`GET nest/api/tutors/all/`

Выполняет поиск в Redis по ключу tutors, если не найдены получает данные из коллекции Tutors, API ID: tutor. Сортировка по возрастанию. Если в Strapi для преподавателя явно указано значение ShowInSite: true, он не будет добавлен в вывод. Это необходимо для случая, когда информацию о преподавателе необходимо отображать только в административной панели.

Выходные данные: +Tutors, API ID: tutor

```json
{
  id: number;
  fio: string;
  about: string;
  position: string;
  published_at: string;
  created_at: string;
  updated_at: string;
  code: string;
  showInSite: boolean;
  fields: TutorFields[];
  meta?: Meta;
}
```

TutorFields:

```json
{
  id: number;
  value: string;
}
```

### Получить список преподавателей 2

`GET nest/api/tutors/study/all/`

Аналогично [[#Получить список преподавателей]] ключ Redis `tutors-study`

Не совсем понятно зачем нужно.

### Получение подробной информации о преподавателе

`GET nest/api/tutors/detail/:code`

В URL запроса должен быть передан код преподавателя

Ищет данные в Redis по ключу tutor:${code}, если нет получает данные из коллекции Strapi Tutors, API ID: tutor по указанному коду

Если преподаватели не найдены, выбрасывается исключение NotFoundException с сообщением "Tutor not found"

Возвращает объект с информацией об учителе, описанный в Strapi.