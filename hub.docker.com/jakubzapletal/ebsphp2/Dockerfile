FROM ubuntu:14.04

RUN \
    apt-get update \
    && apt-get install -y --no-install-recommends \
        software-properties-common \
        make \
        wget \
        g++ \
    && rm -rf /var/lib/apt/lists/*

RUN \
    LC_ALL=C.UTF-8 add-apt-repository ppa:ondrej/php \
    && apt-get update \
    && apt-get install -y --force-yes --no-install-recommends \
        php7.0 \
        php7.0-simplexml \
        php7.0-pgsql \
        php7.0-mbstring \
        postgresql-client \
    && rm -rf /var/lib/apt/lists/*
