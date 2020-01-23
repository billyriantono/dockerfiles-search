FROM tiangolo/uwsgi-nginx-flask:python3.6-alpine3.7

LABEL maintainer="Sergey Sobko <ssobko@hse.ru>"

COPY ./requirements.txt /requirements.txt

RUN apk add --no-cache --virtual .build-deps g++ gcc build-base libxslt-dev libffi-dev mariadb-dev \
    && pip install -r /requirements.txt \
    && apk add --virtual .runtime-deps mariadb-client-libs curl \
    && apk del .build-deps
