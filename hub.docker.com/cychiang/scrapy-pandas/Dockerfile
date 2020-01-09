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

RUN pip install \
    --no-cache-dir \
    pandas==0.20.3 \
    googleads==12.2.0 \
    bottle==0.12.13 \
    requests==2.19.1 \
    Scrapy==1.5.0 \
    beautifulsoup4==4.6.0 \
    bs4==0.0.1 \
    scrapy-splash==0.7.2

RUN apk del .build-deps
