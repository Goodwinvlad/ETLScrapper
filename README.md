### Тестовое задание:

Необходимо написать скрипт который будет ходить в википедию,
и итеративно собирать информацию о городах 
(можно использовать Selenium или Beautifulsoup на выбор)

Список городов - 
Москва, Санкт-Петербург, Омск, Тимашевск, Хельсинки, Икаалинен,  Учкудук, Янгиабад.

Поля которые необходимо забирать : 
Навазние города, Страна , Дата основание, Тип климата, 
Часовой пояс, Население, Плотность населения, Телефонный код , Почтовый индекс

После этого данные необходимо очищать мусора и приводить к общему виду, 
так же необходимо обогащать каждый забор данных датой и временем. (реализация на pandas)
На последнем этапе необходимо поднять базу данных (mysql/postgres в докере) и записать полученный датафрейм в эту базу данных.
При выключение базы данных нужно сделать так, чтобы данные не терялись.

### Решение:

1. Установить подсистему Windows для Linux WSL через терминал
<code>wsl --install</code>
2. Запустить версию WSL 2
<code>wsl --set-default-version 2</code>
3. Установить платформу [Docker Compose](https://docs.docker.com/get-docker/ "Docker Compose")
4. Установить дистрибутив языков программирования Python [Anaconda](https://www.anaconda.com/download/ "Anaconda")
5. Скачать файлы .env и docker-compose.yml. Из директории, со скаченными файлами в терминале запустить следующую команду:</p>
   <code> docker-compose up</code>. </p> После выполнения команды в Docker будут созданы и запущены контейнеры pgadmin_post_container и postgres_post_container с соотвествующими образами
   postrges-pgadmin_post и postrges-postgres_post.
6. По ссылке пройдем [pgAdmin](http://localhost:5050/browser/#) - инструмент для управления PostgreSQL через веб-интерфейс.</p> 
   Для входа используем данные из файла .env</p>  PGADMIN_DEFAULT_EMAIL=*******   PGADMIN_DEFAULT_PASSWORD=*****
7. Создадим сервер со следующими параметрами:</p>  Name = DB_1</p>  Host_name = postgres_post</p>  port = 5432</p>  Maintenance_database = db_test</p>  Username = postgres</p> 
8. В директории DB_1/Databases/db_test/Schemas/public/Tables в [pgAdmin](http://localhost:5050/browser/#) хранятся таблицы. На данном этапе сервер Postgres готов для записи таблиц.
9. Запускаем Jypiter Notebook
10. Запускаем команду и устанавливаем зависимости для проекта</p> 
<code>pip install -r requirements.txt</code>
10. Запускаем код **cities_stat_from_Wikipedia.ipynb**

### Результат:
DataFrame со списком городов. Таблица записана на поднятую БД postgres в Docker. Так же реализовано обращение к БД и запись в DataFrame в Notebook.
Размер DataFrame (8 строк, 10 колонок)
| Column        | Type            |
|:------------- |:---------------:|
| city          | object          |
| Country       | object          |
| Founded       | object          |
| Climate       | object          |
| UTC           | int64           |
| Population    | int64           |
| Phonecode     | object          |
| Postcode      | object          |
| Date          | datetime64[ns]  |
| Timestamp     | float64         |
