FROM python:3.7-alpine

RUN apk update \
  && apk add --virtual build-deps gcc musl-dev \
  && apk add postgresql-dev

RUN pip3 install psycopg2

RUN apk del build-deps