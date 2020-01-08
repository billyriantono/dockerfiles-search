FROM php:7.3.5-fpm-alpine3.9

MAINTAINER srsergey.ivanenko@gmail.com

RUN echo 'http://dl-cdn.alpinelinux.org/alpine/v3.8/main' >> /etc/apk/repositories \
    && apk add --no-cache \
       $PHPIZE_DEPS \
       make \
       git curl nano vim wget \
       freetype libpng libjpeg-turbo freetype-dev libpng-dev libjpeg-turbo-dev libwebp-dev libzip-dev \
       pcre-dev \
       'hiredis-dev=0.13.3-r1' \
       libldap \
       postgresql-dev \
       icu-dev libxml2-dev \
       openldap-dev \
       unzip \
       autoconf \
       tzdata \
       rabbitmq-c rabbitmq-c-dev \
    && docker-php-ext-configure intl \
    && docker-php-ext-configure ldap \
    && docker-php-ext-configure gd \
    && docker-php-ext-install \
        exif \
        mysqli \
        pdo_mysql \
        pdo_pgsql \
        zip \
        bcmath \
        pcntl \
        soap \
        gd \
        ldap \
        pgsql \
        intl \
        sockets \
    && pecl install oauth \
    && docker-php-ext-enable oauth \
# Redis
    && pecl install redis \
    && docker-php-ext-enable redis \
# Amqp
    && pecl install amqp \
    && docker-php-ext-enable amqp \
# Composer
    && cd /var/tmp && wget https://getcomposer.org/composer.phar \
    && cp /var/tmp/composer.phar /usr/local/bin/composer \
    && chmod +x /usr/local/bin/composer \
#Phpiredis
    && cd /var/tmp && git clone https://github.com/nrk/phpiredis.git \
    && cd phpiredis \
    && phpize \
    && ./configure --enable-phpiredis \
    && make \
    && make install \
    && docker-php-ext-enable phpiredis \
#Swoole
    && cd /tmp \
    && git clone https://github.com/swoole/swoole-src.git \
    && cd swoole-src \
    && git checkout v4.3.4 \
    && phpize \
    && ./configure --enable-openssl --enable-sockets --enable-mysqlnd --enable-http2 \
    && make \
    && make install \
    && docker-php-ext-enable swoole \
#Swoole async-ext
    && git clone https://github.com/swoole/async-ext.git \
    && cd async-ext \
    && git checkout tags/v4.3.3 \
    && phpize \
    && ./configure \
    && make \
    && make install \
    && docker-php-ext-enable swoole_async \
#Cleaning
    && apk del make $PHPIZE_DEPS autoconf && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* /var/cache/apk/*

WORKDIR /var/www