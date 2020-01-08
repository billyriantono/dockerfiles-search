FROM python:3.7-alpine
MAINTAINER PYTHON LTD

ENV PYTHONUNBUFFERED 1

COPY ./requerimiento.txt ./requerimiento.txt
RUN pip install -r /requerimiento.txt

RUN mkdir /app
WORKDIR /app
COPY /app /app

RUN adduser -D user
USER user
