# docker build --rm -t pengshaw/gstar .
FROM python:3.7-alpine
MAINTAINER <PengShaw, hhxp9106@gmail.com>

RUN pip install pipenv
WORKDIR /home/gstar
COPY Pipfile* ./

RUN apk add curl vim

RUN apk add --update --no-cache mariadb-connector-c-dev \
    && apk add --no-cache --virtual .build-deps \
        mariadb-dev \
        openssl \
        ca-certificates \
        g++ \
        gcc \
        musl-dev \
    && pipenv install --system --deploy \
    && apk del .build-deps

COPY . .
