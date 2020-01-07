FROM python:3.7-alpine

LABEL maintainer Guilherme Scaranse <guiscaranse@gmail.com>

RUN apk --update add build-base gcc python3-dev musl-dev libffi-dev && \
    rm -rf /var/lib/apt/lists/* && \
    rm /var/cache/apk/*

RUN pip install cython pandas numpy
