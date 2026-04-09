# Blog (Django + DRF)

Учебно-практический проект блога на Django с веб-интерфейсом и REST API.

## Возможности

- Публикация постов, теги, комментарии
- Поиск постов (`/search/`)
- Отдельные страницы постов по дате и `slug`
- Share поста по email
- Sitemap (`/sitemap.xml`)
- OAuth авторизация (GitHub / Google / Yandex)
- REST API для постов
- OpenAPI схема + Swagger UI + Redoc

## Стек

- Python 3.12+
- Django 6
- Django REST Framework
- PostgreSQL
- `django-taggit`
- `django-filter`
- `drf-spectacular`
- `social-auth-app-django`
- `python-dotenv`

## Структура проекта

- `blog_site/` — Django-проект
- `blog_site/blog/` — веб-приложение блога (шаблоны, views, модели)
- `blog_site/blog_api/` — API-приложение (serializers, views, permissions)
- `.env.example` — переменные окружения

## Переменные окружения

Используй шаблон `.env.example` в корне `blog` (рядом с `requirements.txt`).

Скопируй его в локальный `.env` и заполни своими значениями:

```bash
copy .env.example .env
```

Пример содержимого `.env.example`:

```env
DJANGO_SECRET_KEY=change-me
DJANGO_DEBUG=True
ALLOWED_HOSTS=127.0.0.1,localhost
CSRF_TRUSTED_ORIGINS=http://127.0.0.1:8000,http://localhost:8000

DB_ENGINE=django.db.backends.postgresql
DB_NAME=blog_db
DB_USER=postgres
DB_PASSWORD=postgres
DB_HOST=127.0.0.1
DB_PORT=5432

EMAIL_HOST=smtp.example.com
EMAIL_HOST_USER=example@example.com
EMAIL_HOST_PASSWORD=secret
EMAIL_PORT=587
EMAIL_USE_TLS=True

SOCIAL_AUTH_GITHUB_KEY=
SOCIAL_AUTH_GITHUB_SECRET=
SOCIAL_AUTH_GOOGLE_OAUTH2_KEY=
SOCIAL_AUTH_GOOGLE_OAUTH2_SECRET=
SOCIAL_AUTH_YANDEX_OAUTH2_KEY=
SOCIAL_AUTH_YANDEX_OAUTH2_SECRET=
```

## Локальный запуск

Из директории `blog`:

```bash
python -m venv venv
venv\Scripts\activate
pip install -r requirements.txt
cd blog_site
python manage.py migrate
python manage.py createsuperuser
python manage.py runserver
```

Для Linux/macOS активация venv:

```bash
source venv/bin/activate
```

## Основные URL

### Web

- `/` — список постов
- `/search/` — поиск
- `/tag/<slug>/` — посты по тегу
- `/<year>/<month>/<day>/<slug>/` — страница поста
- `/<post_id>/share/` — отправка поста по email
- `/<post_id>/comment/` — добавление комментария
- `/sitemap.xml` — sitemap

### Auth

- `/accounts/` — локальные auth-url
- `/oauth/` — social auth (GitHub / Google / Yandex)

### API

- `/api/` — список/создание постов
- `/api/<id>/` — детали/обновление/удаление поста
- `/api/user/<id>/` — посты конкретного пользователя
- `/api/schema/` — OpenAPI schema
- `/api/schema/swagger-ui/` — Swagger UI
- `/api/schema/redoc/` — Redoc
- `/api-auth/` — login для DRF browsable API

## Авторизация в API

В проекте настроены:

- Session Authentication
- Token Authentication

Также в `REST_FRAMEWORK` по умолчанию стоит `IsAuthenticated`, поэтому для части запросов нужна авторизация.

## Полезные команды

```bash
python manage.py makemigrations
python manage.py migrate
python manage.py collectstatic --noinput
python manage.py shell
```

## План развития

- Добавить покрытие тестами (unit + integration)
- Подготовить Docker/docker-compose для dev
- Добавить CI (lint + tests)
