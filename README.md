# Docker-Compose for Django, Celery and NGinX

- based on: https://saasitive.com/tutorial/django-celery-redis-postgres-docker-compose/

- create venv: python3 -m venv venv; source venv/bin/activate; pip install -r requirements.txt

#  Django start
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

# Docker-compose

- you need to start docker on your machine: `open -a docker`
- docker-compose build
- docker-compose up
- production: docker-compose up --build -d
- to stop: docker-compose down
- IMPORTANT: The docker-compose is running at 0.0.0.0. Just enter this address in your web broswer to play with your web application.

# Git

create git repo from dir

- create new repo in web
- then:
    git init
    git add .
    git commit -m "first commit"
    git branch -M main
    git remote add origin git@github.com:exitfromparadise/docker-compose-django-celery.git
    git push -u origin main


# GUnicorn

- install: python -m pip install gunicorn
- local start: gunicorn myproject.wsgi
- https://docs.gunicorn.org/en/stable/run.html
- https://docs.djangoproject.com/en/4.1/howto/deployment/wsgi/gunicorn/
