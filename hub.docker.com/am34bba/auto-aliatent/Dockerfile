FROM alpine
MAINTAINER Alvaro Lizama Molina <hola@alvarolizama.net>
RUN apk update && apk upgrade \
    && apk add gcc g++ linux-headers musl musl-dev python py-pip \
    && apk add python-dev libffi-dev libxslt-dev libxml2-dev zlib-dev \
    && apk add jpeg-dev libpng-dev postgresql-dev \
    && rm -rf /var/cache/apk/*
