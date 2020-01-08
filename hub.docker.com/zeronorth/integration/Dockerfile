FROM zeronorth/base-python-image:3.6-alpine

MAINTAINER ZeroNorth, Inc.

WORKDIR /app
ADD . /app

RUN apk add --update build-base curl-dev docker gcc libffi-dev make musl-dev \
    python3 python3-dev unzip ca-certificates \
    && pip install --upgrade pip \
    && pip install awscli==1.16.231 cryptography \
    && make docker_deps docker_install \
    && apk del build-base gcc python3-dev \
    && mkdir -p /code \
    && mkdir -p /results \
    && rm -f ~/.pypirc

ENV REQUESTS_CA_BUNDLE=/etc/ssl/certs/ca-certificates.crt

VOLUME /code
VOLUME /results
VOLUME /usr/local/share/ca-certificates
