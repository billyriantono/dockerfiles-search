FROM python:3.6.2-alpine

RUN apk update
RUN apk add --no-cache --virtual .build-deps \
    g++ \
    gcc \
    build-base \
    libxml2-dev \
    libffi-dev \
    libxslt-dev \
    openssl-dev

RUN pip install --no-cache-dir pandas==0.20.3 
