FROM python:2-alpine
MAINTAINER Oscar Prieto <oscarmpp@gmail.com>

RUN apk add --update --no-cache \
    imagemagick \
    curl-dev \
    tzdata

RUN pip --no-cache-dir install -U \
    pip \
    six \
    selenium \
    unidecode \
    requests \
    influxdb \
    robotframework \
    robotframework-appiumlibrary \
    robotframework-seleniumlibrary \
    robotframework-browsermobproxylibrary \
    robotframework-requests
