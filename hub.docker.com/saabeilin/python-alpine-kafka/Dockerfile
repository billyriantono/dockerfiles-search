FROM python:3.6.2-alpine3.6

RUN apk add --no-cache --virtual .deps \
      ca-certificates \
      libressl \
      libressl-dev \
      git \
      g++ \
      make \
      musl-dev \
      zlib-dev \
      librdkafka \
      librdkafka-dev

ENV PYTHONUNBUFFERED 1

COPY requirements.txt /tmp/
RUN pip install --no-cache-dir -r /tmp/requirements.txt
