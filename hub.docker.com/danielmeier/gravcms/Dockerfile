FROM php:7.2-fpm-alpine
MAINTAINER "Dan Meier"
LABEL name="grav-docker-compose"
LABEL version="0.2"

RUN apk update \
    && apk upgrade \
    && apk add --no-cache \
        freetype \
        libpng \
        libjpeg-turbo \
        freetype-dev \
        libpng-dev \
        jpeg-dev \
        libjpeg \
        libjpeg-turbo-dev

RUN docker-php-ext-configure gd \
        --with-freetype-dir=/usr/lib/ \
        --with-png-dir=/usr/lib/ \
        --with-jpeg-dir=/usr/lib/ \
        --with-gd

RUN NUMPROC=$(grep -c ^processor /proc/cpuinfo 2>/dev/null || 1) \
    && docker-php-ext-install -j${NUMPROC} gd

RUN docker-php-ext-install zip
VOLUME /var/www/html
ENV SOURCE="/usr/src/grav"

RUN set -ex; \
  wget https://getgrav.org/download/core/grav-admin/latest && \
  unzip latest && \
  mkdir -p "$SOURCE" && \
  cp -r grav-admin/. "$SOURCE" && \
  rm -rf grav-admin latest && \
  chown -R www-data:www-data "$SOURCE"
