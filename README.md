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
Создайте и заполните базу данных:
```
docker-compose exec web python manage.py migrate
docker-compose exec web python manage.py loaddata dump.json
```
