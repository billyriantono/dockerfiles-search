FROM python:3.4-alpine

MAINTAINER Sergey Berebko <serbernar1@gmail.com>

ENV PYTHONUNBUFFERED 1

RUN apk add --no-cache ca-certificates \
    musl-dev \
    musl-utils \
    musl-dbg \
    gcc \
    libevent-dev \
    python3-dev \
    libxml2-dev \
    libxslt-dev \
    libffi-dev \
    openssl-dev; \
    rm  -rf /tmp/* /var/cache/apk/*
RUN cp -r /usr/include/libxml2/libxml/ /usr/include
COPY requirements.txt /tmp/requirements.txt
RUN pip install --no-cache-dir -r /tmp/requirements.txt

EXPOSE 6800

CMD scrapyd