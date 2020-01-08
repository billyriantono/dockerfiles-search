FROM python:stretch
LABEL maintainer="ntkomata <ntkomata@outlook.com>"
ENV GIT_REPO_URL https://github.com/gothinkster/django-realworld-example-app.git
ENV PORT 8000
ENV PROJECT_NAME conduit

CMD git clone ${GIT_REPO_URL} /var/proj && cd /var/proj && python3 -m pip install -r requirements.txt && python3 -m pip install gunicorn && python3 manage.py makemigrations && python3 manage.py migrate && gunicorn ${PROJECT_NAME}.wsgi -b 0.0.0.0:${PORT} --reload