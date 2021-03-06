FROM php:7.1-fpm-alpine
LABEL maintainer="jonathan <jonathan@webtools.co.nz>"

WORKDIR /app

ENV PHP_XDEBUG_REMOTE_ENABLE=${PHP_XDEBUG_REMOTE_ENABLE:-on}
ENV PHP_XDEBUG_REMOTE_AUTOSTART=${PHP_XDEBUG_REMOTE_AUTOSTART:-on}
ENV PHP_XDEBUG_DEFAULT_ENABLE=${PHP_XDEBUG_DEFAULT_ENABLE:-off}
ENV PHP_XDEBUG_REMOTE_HOST=${PHP_XDEBUG_REMOTE_HOST:-docker.for.mac.localhost}
ENV PHP_XDEBUG_REMOTE_PORT=${PHP_XDEBUG_REMOTE_PORT:-9000}
ENV PHP_XDEBUG_REMOTE_CONNECT_BACK=${PHP_XDEBUG_REMOTE_CONNECT_BACK:-off}
ENV PHP_XDEBUG_IDEKEY=${PHP_XDEBUG_IDEKEY:-PHPSTORM}

# Install system packages
RUN apk update && \
    apk add --no-cache \
        bash \
        git \
        freetds \
        freetype \
        icu \
        libintl \
        libldap \
        libjpeg \
        libmcrypt \
        libpng \
        libpq \
        libwebp \
        libmemcached \
        curl \
        imagemagick \
        composer && \
    apk add --no-cache --virtual build-dependencies \
        curl-dev \
        freetds-dev \
        freetype-dev \
        gettext-dev \
        icu-dev \
        jpeg-dev \
        libmcrypt-dev \
        libpng-dev \
        libmemcached-dev \
        libwebp-dev \
        libxml2-dev \
        openldap-dev \
        postgresql-dev \
        imagemagick-dev \
        zlib-dev \
        autoconf \
        build-base && \
# Install PHP extensions
    docker-php-ext-configure gd \
        --with-freetype-dir=/usr/include/ \
        --with-png-dir=/usr/include/ \
        --with-jpeg-dir=/usr/include/ && \
    docker-php-ext-configure bcmath && \
    docker-php-ext-configure ldap --with-libdir=lib/ && \
    docker-php-ext-configure pdo_dblib --with-libdir=lib/ && \
    docker-php-ext-install \
        bcmath \
        curl \
        gettext \
        gd \
        exif \
        iconv \
        intl \
        ldap \
        mbstring \
        opcache \
        pdo_mysql \
        pdo_pgsql \
        pdo_dblib \
        soap \
        sockets \
        zip && \
# Install PECL extensions
    pecl install xdebug grpc imagick memcached && \
    docker-php-ext-enable xdebug grpc imagick memcached && \
    echo "xdebug.remote_enable=${PHP_XDEBUG_REMOTE_ENABLE}" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini && \
    echo "xdebug.remote_autostart=${PHP_XDEBUG_REMOTE_AUTOSTART}" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini && \
    echo "xdebug.default_enable=${PHP_XDEBUG_DEFAULT_ENABLE}" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini && \
    echo "xdebug.remote_host=${PHP_XDEBUG_REMOTE_HOST}" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini && \
    echo "xdebug.remote_port=${PHP_XDEBUG_REMOTE_PORT}" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini && \
    echo "xdebug.remote_connect_back=${PHP_XDEBUG_REMOTE_CONNECT_BACK}" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini && \
    echo "xdebug.idekey=${PHP_XDEBUG_IDEKEY}" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini && \
    echo "xdebug.remote_log=/tmp/xdebug.log" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini && \
# Install fxp composer plugin
    composer global require "fxp/composer-asset-plugin" && \
    apk del build-dependencies && \
# Download trusted certs
    mkdir -p /etc/ssl/certs && update-ca-certificates

ADD config/php.ini /usr/local/etc/php/php.ini
