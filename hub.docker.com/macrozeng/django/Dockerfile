FROM python:2.7
MAINTAINER Marco Zeng

# create directory which can be a place for generated static content
# volume can be used to serve these files with a webserver
RUN mkdir -p /var/www/static
VOLUME /var/www/static

# create directory which can be a place for user-uploaded files
# volume can be used to serve these files with a webserver
RUN mkdir -p /var/www/media
VOLUME /var/www/media

# create directory for application source code
# volume can be used for live-reload during development
RUN mkdir -p /usr/django/app
VOLUME /usr/django/app

# set default port
ENV PORT=8000

ENV DJANGO_VERSION=1.8.19
RUN pip install mysqlclient
RUN pip install django==$DJANGO_VERSION

WORKDIR /usr/django/app

CMD ["python", "manage.py", "runserver", "0.0.0.0:8000"]
