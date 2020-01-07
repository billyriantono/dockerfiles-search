# 12-09-2019

FROM python:alpine

ENV PYTHONUNBUFFERED 1

RUN apk update \
  && apk add --no-cache --virtual build-deps gcc python3-dev musl-dev \
  && apk add --no-cache postgresql-dev \
  && pip install --no-cache-dir --upgrade pip \
  && pip install --no-cache-dir psycopg2 pyyaml gunicorn django \
    django-htmlmin django_compressor csscompressor django-storages boto3 \
    django-debug-toolbar \
  && apk del build-deps \
  && mkdir -p /webapp/var/cache /webapp/var/logs /webapp/static /webapp/media && \
  rm -f /var/cache/apk/*

WORKDIR /webapp/

EXPOSE 8000
