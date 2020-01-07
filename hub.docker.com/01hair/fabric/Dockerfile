FROM python:2.7-alpine

RUN apk add --no-cache --virtual .build-dependencies gcc musl-dev libffi-dev make openssl-dev \
    && apk add --no-cache libffi openssl openssh-client \
    && pip install fabric==1.14.1 \
    && apk del .build-dependencies
