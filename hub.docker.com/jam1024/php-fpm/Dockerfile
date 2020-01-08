FROM php:7.2-fpm-alpine

MAINTAINER Jam <810441377@qq.com>

RUN apk update \
  && apk add --no-cache \
  tzdata curl \
  libmemcached-dev \
  postgresql-dev \
  freetype-dev \
  libjpeg-turbo-dev \
  libpng-dev

RUN docker-php-ext-install bcmath pcntl pdo_mysql pdo_pgsql mysqli opcache \
  && docker-php-ext-configure gd \
    --with-jpeg-dir=/usr/lib \
    --with-freetype-dir=/usr/include/freetype2 \
  && docker-php-ext-install gd \
  && apk del autoconf \
  g++ make \
  openssl-dev \
  && rm -rf /var/cache/apk/*
