FROM python:3.6.0-alpine

RUN apk update && \
	apk add python \
        python3 \
        python3-dev \
        supervisor \
        postgresql-dev \
        build-base \
        jpeg-dev \
        zlib-dev \
        libffi-dev

RUN pip install --upgrade pip && \
    pip install grpcio && \
    pip install grpcio-tools && \
    pip install --upgrade setuptools

RUN pip install cryptography \
                cffi \
                psycopg2
