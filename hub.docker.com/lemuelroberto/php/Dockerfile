FROM php:7.3-fpm-alpine3.9

MAINTAINER Arquivei

RUN set -xe \
    \
# Install build dependencies
    && apk --no-cache --virtual .build-deps add \
        autoconf \
        bash \
        build-base \
        pcre-dev \
        python \
# Install PHP extensions dependencies
    && apk --no-cache add \
        libzip-dev \
        libxml2-dev \
        postgresql-dev \
    \
    && docker-php-ext-install \
# Install PHP bcmath extension
        bcmath \
# Install PHP pdo_pgsql extension
        pdo_pgsql \
# Install PHP pgsql extension
        pgsql \
# Install PHP soap extension
        soap \
# Install PHP zip extension
        zip \
    \
# Build, install and enable PHP rdkafka extension
    && mkdir -p /tmp/librdkafka \
    && cd /tmp/librdkafka \
    && curl -L https://github.com/edenhill/librdkafka/archive/v1.0.1.tar.gz | tar xz \
    && cd librdkafka-1.0.1 \
    && ./configure \
    && make \
    && make install \
    && pecl install rdkafka \
    && docker-php-ext-enable rdkafka \
    && rm -rf /tmp/librdkafka \
# Remove build dependencies
    && apk del .build-deps
