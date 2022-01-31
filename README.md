# skyeng1-otus


Сервис обеспечивает хранение данных о выполнении студентом учебных заданий. Имеется спектр возможных для обучения навыков. Для каждого задания задаётся распределение спектра навыков с долями (например, задание «диалог с преподавателем на английском языке» тренирует навык говорения на 70% и навык аудирования на 30%). Задание оценивается в баллах в некотором диапазоне (например, от 1 до 10), баллы распределяются по навыкам пропорционально. Задания группируются в занятия, занятия группируются в курсы (также возможны промежуточные уровни: например, модули внутри курса). Сервис должен решать следующие задачи:

·        Хранение баллов за каждое задание

·        Агрегация баллов за задания по занятиям и навыкам

·        Агрегация баллов по времени

·        Агрегация баллов по курсам (и промежуточным уровням, при наличии)

·        Выдача ачивок за выполнение различных условий (например, «все задания в занятии выполнены на 10 баллов», «доля оценок выше 9 больше 90%» и т.п.)

Сохранение баллов должно выполняться в асинхронном режиме. Необходимо продумать схему кэширования агрегированных данных.

Опционально: продумать GraphQL-реализацию API для получения агрегации.


---------
app.local

```shell
cp .env.example .env
cp code/.env.example code/.env
docker-compose build
docker-compose up -d
docker-compose exec --user=1000:1000 php bash #1000 - user id & group id
#>>
cd /data
composer install
php artisan migrate
php artisan db:seed

#ln -s vendor/swagger-api/swagger-ui/dist/ public/swagger-ui-assets
cp -r vendor/swagger-api/swagger-ui/dist/ public/swagger-ui-assets

cd /data/console
php console.php student_task_rate & \
php console.php student_aggregation_tasks_skills & \
php console.php student_aggregation_time_today & \
php console.php student_aggregation_time_month & \
php console.php student_aggregation_courses & \
php console.php student_receive_awards &
```

## Swagger
<host>/api/documentation - swagger
```shell
php artisan swagger-lume:publish # to publish everything - once after install swagger
php artisan swagger-lume:generate # to generate docs
```
Скопировать содержимое папки `/vendor/swagger-api/swagger-ui/dist/`  
в `public/swagger-ui-assets` (или сделать симлинк)
  
## run tests
```shell
# cd code
phpunit
```



### Проектная работа выполнена для курса "[PHP Developer. Professional](https://otus.ru/lessons/razrabotchik-php/)"
