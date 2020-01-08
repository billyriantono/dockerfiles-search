FROM php:5.6-fpm-alpine
MAINTAINER Mike George <mgeorge@mreach.com>

ENV COMPOSER_ALLOW_SUPERUSER=true

# PHP Extensions (gd, pdo, pdo_pgsql, opcache, zip)
RUN apk add --no-cache postgresql-dev freetype-dev libpng-dev libjpeg-turbo-dev freetype libpng libjpeg-turbo && \
  docker-php-ext-configure gd \
  --with-gd \
  --with-freetype-dir=/usr/include/ \
  --with-png-dir=/usr/include/ \
  --with-jpeg-dir=/usr/include/ && \
  NPROC=$(grep -c ^processor /proc/cpuinfo 2>/dev/null || 1) && \
  docker-php-ext-install -j${NPROC} gd pdo pdo_pgsql opcache zip && \
  apk del --no-cache freetype-dev libpng-dev libjpeg-turbo-dev

# Composer for managing deps
RUN apk add --no-cache curl git zip unzip && \
  curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

WORKDIR /var/www
