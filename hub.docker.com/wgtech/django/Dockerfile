FROM wgtech/python:easy-dev

ENV DJANGO_VERSION 2.1.7

RUN pip install --upgrade --ignore-installed pip setuptools
RUN pip install django==$DJANGO_VERSION

# Recommend directory for making your an django app.
RUN mkdir -p /app/django

WORKDIR /app/django

# If you want to start new django app, just type commands below.
#
# 1) django-admin startproject YOUR-APP-NAME /app/django
# 2) python manage.py migrate
# 3) python manage.py runserver

EXPOSE 8000

ENTRYPOINT [ "/bin/bash" ]