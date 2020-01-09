FROM php:7.1-fpm-alpine

RUN apk add --no-cache freetype libpng libjpeg-turbo freetype-dev libpng-dev libjpeg-turbo-dev && \
  docker-php-ext-configure gd \
    --with-gd \
    --with-freetype-dir=/usr/include/ \
    --with-png-dir=/usr/include/ \
    --with-jpeg-dir=/usr/include/ && \
  docker-php-ext-install gd && \
  apk del --no-cache freetype-dev libpng-dev libjpeg-turbo-dev && \
  apk add --no-cache gmp gmp-dev && \
  docker-php-ext-install gmp && \
  apk del --no-cache gmp-dev
