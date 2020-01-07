FROM python:3.6-alpine
RUN apk update \
 && apk add postgresql-libs \
 && apk add --virtual .devdeps postgresql-dev musl-dev gcc \
 && pip install -U pip pipenv

COPY Pipfile Pipfile.lock /

RUN set -ex && pipenv install --system --deploy \
 && rm /Pipfile /Pipfile.lock \
 && apk del .devdeps \
 && rm -rf /var/cache/apk/*
