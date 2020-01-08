FROM python:3.7.4-alpine

LABEL maintainer="Roberto Chaud"
LABEL version="0.2"

ENV PYTHONUNBUFFERED 1
ENV PYTHONDONTWRITEBYTECODE 1

RUN mkdir -p /var/django/app
WORKDIR /var/django/app

COPY requirements.txt /

RUN apk add --no-cache build-base \
                       postgresql-client \
                       postgresql-dev \
                       libldap \
                       openldap-clients \
                       libffi-dev \
                       openldap-dev \
                       musl-dev \
                       git

RUN pip install --no-cache-dir pip --upgrade

RUN pip install --no-cache-dir -r /requirements.txt

