FROM python:3.7-alpine3.8
MAINTAINER Homicity Ltd.

ENV PYTHONUNBUFFERED 1
ENV DEBIAN_FRONTEND noninteractive

# postgresql-client is required by psql
# postgresql-dev musl-dev gcc are required by psycopg
# NOTE: there is py3-psycopg2
# gdal-dev geos-dev proj4-dev are required by geodjango
# NOTE: we actually need gdal-dev not gdal

ENV ALPINE_MIRROR "http://dl-cdn.alpinelinux.org/alpine"
RUN echo "${ALPINE_MIRROR}/edge/main" >> /etc/apk/repositories
RUN apk add --update libressl2.7-libcrypto

# Install dependencies
RUN apk update && apk upgrade \
    && apk add postgresql-client postgresql-dev musl-dev gcc \
    && apk add --repository http://dl-cdn.alpinelinux.org/alpine/edge/testing \
        gdal-dev \
        geos-dev \
        proj4-dev

COPY ./requirements.txt /requirements.txt
RUN pip install -r /requirements.txt

# Setup directory structure
RUN mkdir /app
WORKDIR /app
COPY ./app/ /app

RUN adduser -D user
USER user

# Port to expose
EXPOSE 8000
# Copy entrypoint script into the image