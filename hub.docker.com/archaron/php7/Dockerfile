################################################################################
# Base image
################################################################################

FROM php:7.4.0RC1-fpm-alpine

################################################################################
# Build instructions
################################################################################

ENV TERM xterm
ENV ROOT_PASSWORD "root"


RUN apk add --update --no-cache --virtual .build-deps \
        freetype-dev \
        jpeg-dev \
        libxpm-dev \
        libtool \
        coreutils \
        openssl-dev \
        icu-dev \
        autoconf \
        automake \
		file \
		g++ \
		gcc \
		libc-dev \
		make \
		pkgconf \
		re2c \
        imagemagick-dev \
        oniguruma-dev \
        libzip-dev \
    && echo | pecl install -f imagick \
    && echo | pecl install -f mongodb \
    && docker-php-ext-configure \
            gd \
            --with-freetype-dir=/usr/include/ \
            --with-jpeg-dir=/usr/include/ \
            --with-png-dir=/usr/include/ \
            --with-xpm-dir=/usr/include/ \
    && docker-php-ext-install -j$(nproc) \
        iconv \
        gd \
        exif \
        mysqli \
        mbstring \
        pdo \
        pdo_mysql \
        zip \
        intl \
        pcntl \
        opcache \
    && docker-php-ext-enable \
        iconv \
        gd \
        exif \
        mysqli \
        mbstring \
        pdo \
        pdo_mysql \
        zip \
        intl \
        imagick \
        mongodb \
        pcntl \
        opcache \
    && apk del .build-deps \
    && apk add --no-cache \
        imagemagick \
        openssl \
        libx11 \
        icu \
        libxpm \
        nodejs \
        nodejs-npm \
        libzip \
    && rm -rf /var/cache/apk/* \
    && rm -rf /tmp/pear \
    && rm -rf /usr/src


RUN curl -sS https://getcomposer.org/installer | php \
    && mv composer.phar /usr/local/bin/composer \
    && chmod +x /usr/local/bin/composer \
    && rm -rf /var/cache/apk/*

RUN mkdir /project
RUN touch /tmp/docker.txt

RUN composer global require "fxp/composer-asset-plugin:~1.4"
RUN composer global require hirak/prestissimo
RUN composer config --global github-oauth.github.com 248531bddfaca25ef49fd5310073cfa0e6b182a4

RUN /usr/bin/npm -g install bower

RUN apk add --update --no-cache git

RUN echo "memory_limit = 1024M" > /usr/local/etc/php/conf.d/memory_limit.ini