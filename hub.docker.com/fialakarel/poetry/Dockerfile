FROM python:3.8-alpine

MAINTAINER Karel Fiala <fiala.karel@gmail.com>

RUN apk --no-cache add curl \
    && curl -sSL https://raw.githubusercontent.com/python-poetry/poetry/master/get-poetry.py | python

ENV PATH "/root/.poetry/bin:$PATH"
