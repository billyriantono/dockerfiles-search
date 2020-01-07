FROM alpine
MAINTAINER Hajime Kurita / https://twitter.com/hikarine3 / https://en.sakuhindb.com/pe/Administrator/

# Setup
RUN apk update
RUN apk upgrade
RUN apk add --update python3 python3-dev postgresql-client postgresql-dev build-base
# build-base is necessary for build pip modules
# commented out: build-base gettext
RUN pip3 install --upgrade pip
RUN pip3 install django django-environ gunicorn psycopg2

# Clean
RUN apk del -r python3-dev postgresql

ENV PYTHONUNBUFFERED 1
