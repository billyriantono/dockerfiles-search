FROM python:3.6.7-alpine

RUN apk add --update --no-cache --virtual .run-deps \
    libc-dev \
    python3-dev \
    freetds-dev \
    chromium \
    chromium-chromedriver \
    libffi-dev \
    libressl-dev \
    libxml2-dev \
    xmlsec-dev \
    && apk add --update --no-cache --virtual .build-deps \
    g++ \
    gcc \
    && pip install --no-cache-dir cython==0.29.1 \
    && pip install --no-cache-dir \
    azure==3.0.0 \
    pymongo==3.7.1 \
    pymssql==2.1.4 \
    numpy==1.14.5 \
    pandas==0.23.4 \
    lxml==4.3.0 \
    SQLAlchemy==1.2.15 \
    && rm -rf /var/cache/apk/* \
    && apk del .build-deps
