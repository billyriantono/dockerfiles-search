FROM python:3.6-alpine

RUN apk update \
  && apk add --virtual build-deps gcc musl-dev  \
  && apk add libressl-dev libffi-dev

RUN pip3 install pymysql

RUN apk del build-deps
