FROM php:7.1-fpm

RUN apt-get update && \
    apt-get install -y libpq-dev libzip-dev libicu-dev --no-install-recommends && \
    rm -rf /var/lib/apt/lists/* && \
    docker-php-ext-install \
        pdo \
        pdo_pgsql \
        pgsql \
        sockets \
        intl

