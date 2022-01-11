[![yamdb_final workflow](https://github.com/Al-ta-iR/yamdb_final/actions/workflows/yamdb_workflow.yml/badge.svg)](https://github.com/Al-ta-iR/yamdb_final/actions/workflows/yamdb_workflow.yml)

### Описание проекта:

Проект YaMDb собирает отзывы пользователей на различные произведения.

Проект запущен по адресу <http://51.250.24.250/api/v1/>.

Документация по API: <http://51.250.24.250/redoc/>.

### Как запустить проект локально в docker-контейнерах:

Клонировать репозиторий и перейти в него в командной строке:

```
git clone git@github.com:Al-ta-iR/yamdb_final.git
```

```
cd yamdb_final
```

Перейти в папку развёртывания инфраструктуры и подготовить файл переменных окружения .env:

```
cd infra
```

скопировать шаблон из файла .env.template:
```
cp .env.template .env
```

заполнить его следующими данными:
```
SECRET_KEY='Django_SECRET_KEY' # секретный ключ Django (укажите свой)
POSTGRES_DB=postgres # имя базы данных
POSTGRES_USER=postgres # логин для подключения к базе данных
POSTGRES_PASSWORD=postgres # пароль для подключения к БД (установите свой)
DB_HOST=db # название сервиса (контейнера)
DB_PORT=5432 # порт для подключения к БД
```

Запустить приложение в docker-контейнерах:

```bash
docker-compose up -d
```

Выполнить миграции и сбор статики:

```bash
docker-compose exec web python3 manage.py migrate
```
    
```bash
docker-compose exec web python3 manage.py collectstatic --no-input
```

Теперь по адресу <http://127.0.0.1/redoc/> доступна документация по API проекта.

### Создать суперпользователя

```bash
docker-compose exec web python3 manage.py createsuperuser
```

Теперь по адресу <http://127.0.0.1/admin/> доступна админка проекта.

### Заполнить базу начальными данными

```bash
docker-compose exec web python3 manage.py loaddata static/fixtures.json
```

### Остановить работу всех контейнеров

```bash
docker-compose down
```
___________________________________
**Authors:** Artyom Oleynik & *Co*
