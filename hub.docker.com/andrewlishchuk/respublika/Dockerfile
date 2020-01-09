FROM alpine:edge

MAINTAINER Andrew Lishchuk <andrew.lishchuk@gmail.com>


RUN mkdir /app
WORKDIR /app

ARG env=test

ENV ENV=$env


RUN sed -i -e 's/dl-cdn/dl-4/' /etc/apk/repositories && \
    apk update && \
	apk add --no-cache py-psycopg2 \
	python3 \
    py3-pillow

ADD . /app/

RUN pip3 install -r /app/requirements.txt gunicorn

CMD gunicorn -b 0.0.0.0:8000 --reload --forwarded-allow-ips="nginx" app.wsgi
