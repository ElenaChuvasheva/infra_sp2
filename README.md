# Docker-compose для проека YaMDb
Запуск docker-compose для проекта YAMDb, содержащего API сайта с рецензиями на произведения

## Заполнение файла .env
Файл .env создаётся в директории **infra_sp2/infra/** и имеет следующую структуру (вместо значений по умолчанию укажите свои данные):
```
DB_ENGINE=django.db.backends.postgresql
DB_NAME=postgres
POSTGRES_USER=postgres
POSTGRES_PASSWORD=abcd1234
DB_HOST=db
DB_PORT=5432
```
## Запуск проекта
Клонируйте репозиторий и перейдите в папку **infra_sp2/infra/**:
```
git clone <адрес репозитория>
```
```
cd infra_sp2/infra/
```
Создайте файл .env и заполните его (см. выше). Разверните проект:
```
docker-compose up
```
В новом окне консоли перейдите в ту же папку, создайте базу данных и суперюзера, соберите статику:
```
docker-compose exec web python manage.py migrate
docker-compose exec web python manage.py createsuperuser
docker-compose exec web python manage.py collectstatic --no-input
```
Узнайте имя или ID контейнера web:
```
docker container ls
```
Положите файл с тестовыми данными для базы в контейнер:
```
docker cp fixtures.json <имя или ID контейнера web>:/app/
```
Выгрузите данные из fixtures.json в базу данных:
```
docker-compose exec web python manage.py loaddata fixtures.json
```
Зайдите в админку сайта http://localhost/admin/ с указанными ранее логином и паролем для суперюзера.
