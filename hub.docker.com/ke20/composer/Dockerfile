FROM composer

MAINTAINER Kevin Auvinet <k.auvinet@gmail.com>

RUN apk --update add make && \
    rm -rf /var/cache/apk/*

RUN docker-php-ext-install pcntl && \
    rm -rf /var/cache/apk/*
