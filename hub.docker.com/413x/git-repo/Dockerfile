FROM python:3.3-alpine
ENV BUILD_PACKAGES bash curl-dev libxslt-dev libxml2-dev zlib-dev build-base

RUN apk add --no-cache \
    $BUILD_PACKAGES \
    git

RUN pip install lxml

RUN pip install git-repo

ENV LANG=en_US.UTF-8
ENV LANGUAGE=en_US.UTF-8
