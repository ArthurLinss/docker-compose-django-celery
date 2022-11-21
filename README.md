- based on: https://saasitive.com/tutorial/django-celery-redis-postgres-docker-compose/

- create venv: python3 -m venv venv; source venv/bin/activate; pip install -r requirements.txt

Django start
- django-admin startproject backend
- python manage.py startapp assignments
- add "rest_framework" and "assignments" to installed apps in settings
- python manage.py makemigrations; python manage.py migrate

Run locally with Celery (not working with latest settings file but should work with a standard django settings file from a startproject command)

- at end of settings file we need:
    CELERY_BROKER_URL = "redis://localhost:6379/0"
    CELERY_RESULT_BACKEND = "redis://localhost:6379/0"
- go to backend directory, e.g. `/Users/arthur/Documents/private/coding/docker-compose-tutorial/backend`
- first terminal: python manange.py runserver
- 2nd terminal: redis-server
- 3rd terminal: celery -A backend worker --loglevel=info --concurrency 1 -E

Docker-compose

- you need to start docker on your machine: `open -a docker`
- docker-compose build
- docker-compose up
- production: docker-compose up --build -d
- to stop: docker-compose down
