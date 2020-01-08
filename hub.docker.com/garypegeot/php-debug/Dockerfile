FROM composer
FROM php:7.3-cli-alpine

COPY --from=composer /usr/bin/composer /usr/local/bin/composer

RUN apk add --no-cache \
        bash \
        ca-certificates \
        curl \
        icu-libs \
        git \
        unzip \
        zlib-dev && \
    apk add --no-cache --virtual .build-deps \
        $PHPIZE_DEPS \
        curl-dev \
        openldap-dev \
        libxml2-dev \
        libzip-dev \
        icu-dev

RUN docker-php-ext-configure zip --with-libzip && \
    docker-php-ext-install \
        bcmath \
        curl \
        intl \
        ldap \
        pcntl \
        sockets \
        xml \
        zip

RUN pecl install apcu xdebug && \
    docker-php-ext-enable \
        apcu \
        opcache \
        xdebug
