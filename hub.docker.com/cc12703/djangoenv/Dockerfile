
FROM python:3.6-alpine

MAINTAINER morris "cc12703@gmail.com"


RUN apk add --no-cache --update \
	postgresql-libs \
	openjdk7-jre  \
	tzdata



ADD requirements.txt /requirements_base.txt

RUN apk add --no-cache --virtual .build-deps \
        alpine-sdk \
        musl-dev \
        postgresql-dev \
        libressl-dev \
        libffi-dev   && \
    pip install -r /requirements_base.txt  && \
    apk del .build-deps