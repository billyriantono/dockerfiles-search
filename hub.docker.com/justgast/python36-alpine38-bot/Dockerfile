# Use an official Python runtime as a parent image
FROM python:3.6-alpine3.8

WORKDIR /app

COPY requirements-transport.txt /app
COPY requirements-bot.txt /app

RUN apk add --no-cache --virtual .build-deps gcc musl-dev libffi-dev openssl-dev jpeg-dev zlib-dev && \
    apk add libmagic libjpeg-turbo && \
    pip install --upgrade pip && \
    pip install --no-cache-dir --trusted-host pypi.python.org -r requirements-transport.txt && \
    pip install --no-cache-dir --trusted-host pypi.python.org -r requirements-bot.txt && \
    apk del .build-deps

EXPOSE 8080