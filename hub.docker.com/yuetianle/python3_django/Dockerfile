FROM python:3.6-alpine
MAINTAINER OVT
WORKDIR /root/service

COPY requirements.txt .
RUN apk update && apk add --no-cache --virtual .build-deps \
    mariadb-dev \
    gcc \
    musl-dev \
    && apk add bash \
    && pip install -r requirements.txt \
    && apk del .build-deps
EXPOSE 9099/tcp
