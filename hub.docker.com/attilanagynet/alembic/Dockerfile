FROM python:3.7.3-alpine3.9

RUN apk add --update coreutils \
    && rm -rf /var/cache/apk/*

ADD requirements.txt /
RUN pip install -r /requirements.txt

ADD alembic.ini /

ADD start.sh /
CMD ["/start.sh"]

LABEL maintainer="attila@attilanagy.net"
LABEL Description="Alpine based Python image for Alembic PostgreSQL migrations"