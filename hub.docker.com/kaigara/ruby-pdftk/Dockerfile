FROM ruby:2.2-jessie

RUN apt-get update && \
    apt-get install -y \
    poppler-utils \
    poppler-data \
    ghostscript \
    tesseract-ocr \
    tesseract-ocr-fra \
    graphicsmagick \
    pdftk \
    strace \
    curl \
    wget \
    git-core \
    autoconf \
    bison \
    build-essential \
    libssl-dev \
    libyaml-dev \
    libreadline6-dev \
    zlib1g-dev \
    libncurses5-dev \
    libffi-dev \
    libgdbm3 \
    gawk \
    libmysqlclient-dev \
    libtool \
    pkg-config

ARG DOCKERIZE_VERSION=v0.6.1

RUN wget -q https://github.com/jwilder/dockerize/releases/download/${DOCKERIZE_VERSION}/dockerize-linux-amd64-${DOCKERIZE_VERSION}.tar.gz \
    && tar -C /usr/local/bin -xzvf dockerize-linux-amd64-${DOCKERIZE_VERSION}.tar.gz \
    && rm dockerize-linux-amd64-${DOCKERIZE_VERSION}.tar.gz

RUN useradd -u 1000 -m web

VOLUME /home/web
USER web
ENV HOME="/home/web" \
    GEM_HOME="/home/web/.gem" \
    BUNDLE_PATH="/home/web/.gem" \
    PATH="${PATH}:/home/web/.gem/bin" \
    BUNDLE_APP_CONFIG="/home/web/.gem" \
    LANG="en_US.UTF-8" \
    LANGUAGE="en_US.UTF-8"

WORKDIR "/home/web"
