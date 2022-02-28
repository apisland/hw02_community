# Ятюб
## сеть миниблогов
- Создано и зарегистрировано приложение Posts.
- Подключена база данных.
- Десять последних записей выводятся на главную страницу.
- В админ-зоне доступно управление объектами модели Post: можно публиковать новые записи или редактировать/удалять существующие.
- Пользователь может перейти на страницу любого сообщества, где отображаются десять последних публикаций из этой группы.

## Модели (models.py)
Post (запись)
```
Название	Имя поля	Тип поля
Текст	text	Текст
Дата публикации	pub_date	Дата (автоматически добавляется текущая дата)
Автор	author	Ссылка на модель User (связь «один-ко-многим»)
Сообщество	group	Ссылка на модель Group (связь «один-ко-многим»)
```
## Group (сообщество)
```
Название	Имя поля	Тип поля
Имя	title	Строка
Адрес	slug	Поле типа slug
Описание	description	Текст
__str__		Метод __str__ возвращает имя сообщества (title)
```
## Админка (admin.py)
Зарегистрирована модель Group.
Для модели Post создана кастомная админка:
В списке объектов в админке отображаются поля pk, text, pub_date, author, group.
Содержимое поля group можно редактировать в админке прямо в списке объектов Post.
Доступен поиск по полю text.
Доступна фильтрация по полю pub_date.
Если какое-то поле не заполнено, в нём отображается текст -пусто-.
## View-функции (views.py)
index(): передаёт в шаблон posts/index.html десять последних объектов модели Post.
group_posts(): передаёт в шаблон posts/group_list.html десять последних объектов модели Post, отфильтрованных по полю group, и содержимое для тега <title>.
## Адреса (urls.py)
Для приложения Posts установлен namespace='posts'.
Для главной страницы установлен name='index'.
Страница с постами из определённой группы доступна по URL вида group/<slug>/.
Для страницы с постами группы установлен name='group_list'.
## Шаблоны
Файлы шаблонов хранятся на уровне проекта.
Шаблоны разбиты на логические блоки и собираются с помощью тегов include и extend.
К шаблонам подключена статика.
Шаблоны соответствуют дизайну:
web_hw02_community_with_text.zip
В шаблоне index.html ссылка <a href="">все записи группы</a> адресует пользователя на страницу той группы, которой принадлежит пост.
Из view-функций в словаре context передаётся основное содержимое страницы.
Содержимое тега <title> — для разных страниц разное:
```
для страницы группы: Записи сообщества <имя_группы>;
для главной страницы: Последние обновления на сайте.
```

