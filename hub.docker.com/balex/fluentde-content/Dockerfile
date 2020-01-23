FROM php:7.3-fpm-alpine

RUN set -eux; \
    apk add --virtual .buildep --no-cache \
        autoconf \
        g++ \
        make \
    ;

RUN set -eux; \
    apk add --no-cache \
        curl-dev \
        freetype-dev \
        gmp \
        gmp-dev \
        icu-dev \
        libjpeg-turbo-dev \
        libmcrypt-dev \
        libpng-dev \
        libxml2-dev \
        libxslt-dev \
        libzip-dev \
    ;

RUN set -eux; \
    docker-php-ext-configure \
        gd --with-jpeg-dir=/usr/local/ --with-freetype-dir=/usr/include/ \
    ; \
    docker-php-ext-install \
        bcmath \
        gd \
        gmp \
        intl \
        opcache \
        pcntl \
        pdo_mysql \
        soap \
        sockets \
        xsl \
        zip \
    ; \
    pecl install redis; \
    docker-php-ext-enable \
        redis \
    ;

RUN set -eux; \
    apk del .buildep

COPY php.ini-* /tmp/
RUN for mode in development production; do \
        cat /tmp/php.ini-$mode >> $PHP_INI_DIR/php.ini-$mode; \
        rm /tmp/php.ini-$mode; \
    done

RUN set -eux; \
    cp "$PHP_INI_DIR/php.ini-production" "$PHP_INI_DIR/php.ini"
