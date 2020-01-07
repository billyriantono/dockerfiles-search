FROM lucaslsl/alpine-python:latest

RUN apk add --no-cache postgresql-dev

RUN mkdir /tmp/env

COPY requirements.txt /tmp/env/requirements.txt

RUN pip install -r /tmp/env/requirements.txt

