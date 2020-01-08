FROM php:5.6-fpm-alpine

ARG PHP_REDIS_VERSION="4.3.0"
ARG PHP_MONGO_VERSION="1.6.0"
ARG PHP_EXT_DIR="/usr/src/php/ext"

RUN cd /tmp \
    && mkdir -p ${PHP_EXT_DIR} \
    && cd $PHP_EXT_DIR \
    # && sed -i 's/dl-cdn.alpinelinux.org/mirrors.cloud.tencent.com/g' /etc/apk/repositories \
    && apk update \
    && apk add --no-cache --virtual .build-deps2 \
                openssl-dev \
    && apk add --no-cache \
                libpng-dev \
    && wget http://pecl.php.net/get/mongodb-${PHP_MONGO_VERSION}.tgz \
    && wget http://pecl.php.net/get/redis-${PHP_REDIS_VERSION}.tgz \
    && tar zxf redis-${PHP_REDIS_VERSION}.tgz \
    && tar zxf mongodb-${PHP_MONGO_VERSION}.tgz \
    && docker-php-ext-install mongodb-${PHP_MONGO_VERSION} redis-${PHP_REDIS_VERSION} opcache mysqli pdo_mysql sockets gd \
    && docker-php-source delete \
    && apk del .build-deps2 \
    && rm -rf /tmp/* \
    && rm -rf /var/cache/apk
