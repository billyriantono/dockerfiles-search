FROM php:7.1-fpm-alpine

ARG JPEGOPTIM_VERSION=1.4.6

RUN set -xe \
    && apk add --no-cache grep

RUN set -xe \
    && apk add --no-cache freetype libpng libjpeg-turbo freetype-dev libpng-dev libxml2-dev libjpeg-turbo-dev \
    && docker-php-ext-configure gd \
        --with-freetype-dir=/usr/include/ \
        --with-png-dir=/usr/include/ \
        --with-jpeg-dir=/usr/include/ \
    && docker-php-ext-install gd \
    && apk del --no-cache libjpeg-turbo-dev freetype-dev libxml2-dev

RUN set -xe \
    && docker-php-ext-install bcmath

RUN set -xe \
    && apk add --no-cache bzip2-dev \
    && docker-php-ext-install bz2

RUN set -xe \
    && docker-php-ext-install exif

RUN set -xe \
    && apk add --no-cache libintl icu icu-dev \
    && docker-php-ext-install intl \
    && apk del --no-cache icu-dev

RUN set -xe \
    && docker-php-ext-install opcache

RUN set -xe \
    && apk add --no-cache libmcrypt-dev \
    && docker-php-ext-install mcrypt

RUN set -xe \
    && docker-php-ext-install pdo_mysql

RUN set -xe \
    && docker-php-ext-install sockets

RUN set -xe \
    && docker-php-ext-install zip

# Install memcached
RUN set -xe \
    && apk add --no-cache libmemcached-dev zlib-dev cyrus-sasl-dev autoconf g++ make \
    && pecl install memcached \
    && docker-php-ext-enable memcached \
    && apk del --no-cache zlib-dev cyrus-sasl-dev make autoconf g++

# Install Imagick
RUN set -xe \
    && apk add --no-cache imagemagick-dev autoconf g++ libtool make \
    && pecl install imagick \
    && docker-php-ext-enable imagick \
    && apk del --no-cache autoconf g++ libtool make

# Install JPEG-Optim
RUN set -xe \
    && apk add --no-cache alpine-sdk libjpeg-turbo libjpeg-turbo-dev \
    && mkdir -p /usr/src/jpegoptim /source \
    && wget -O - https://github.com/tjko/jpegoptim/archive/RELEASE.${JPEGOPTIM_VERSION}.tar.gz | tar xz -C /usr/src/jpegoptim --strip-components=1 \
    && cd /usr/src/jpegoptim \
    && ./configure --exec-prefix=/usr \
    && make \
    && make strip \
    && make install \
    && rm -rf /usr/src/jpegoptim \
    && apk del alpine-sdk libjpeg-turbo-dev \
    && rm -rf /var/cache/apk/*

# Install PNG-Crush
RUN set -xe \
    && apk add --no-cache pngcrush

# WKHTML
RUN apk add --no-cache \
    libgcc libstdc++ libx11 glib libxrender libxext libintl \
    libcrypto1.0 libssl1.0 \
    ttf-dejavu ttf-droid ttf-freefont ttf-liberation ttf-ubuntu-font-family

# cleanup
RUN set -xe \
    && rm -rf /tmp/* /var/cache/apk/*

WORKDIR /var/www/html

CMD ["php-fpm", "--allow-to-run-as-root", "--pid", "/var/run/php-fpm.pid", "--fpm-config", "/usr/local/etc/php-fpm.conf"]
