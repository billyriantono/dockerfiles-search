FROM gitlab/gitlab-runner:alpine

MAINTAINER FS. <fserafini@itnow.es>

RUN apk add --update --no-cache \
    python \
    python-dev \
    py-pip \
    curl \
    curl-dev \
    imagemagick \
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
