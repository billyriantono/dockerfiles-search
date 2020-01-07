FROM python:2-alpine
MAINTAINER Ozgur Amac

RUN set -ex \
    && apk add --no-cache \
            bash \
            gcc \
            libc-dev \
            libxml2-dev \
            libxslt-dev \
            make \
            musl-dev \
            pcre-dev \
            postgresql-dev \
    && echo Done installing needed packages... \
    && pip install -U pip \
    && echo Done upgrading pip... \
    && CFLAGS="-O0"  pip install lxml \
    && echo Done installing python package lxml... \
    && echo Done!
