# start with the official Composer image and name it
FROM composer:latest AS composer

FROM php:7.2-alpine

ENV PHPREDIS_VERSION 3.0.0

RUN mkdir -p /usr/src/php/ext/redis \
    && curl -L https://github.com/phpredis/phpredis/archive/$PHPREDIS_VERSION.tar.gz | tar xvz -C /usr/src/php/ext/redis --strip 1 \
    && echo 'redis' >> /usr/src/php-available-exts \
    && docker-php-ext-install redis

RUN apk -v --update add \
    docker \
    python \
    py-pip \
    groff \
    less \
    mailcap \
    unzip \
    && \
    docker-php-ext-install bcmath pdo pdo_mysql pcntl \
    && \
    pip install --upgrade awscli==1.14.5 s3cmd==2.0.1 python-magic && \
    apk -v --purge del py-pip && \
    rm /var/cache/apk/*

COPY --from=composer /usr/bin/composer /usr/bin/composer

VOLUME /root/.aws

VOLUME /project

WORKDIR /project
