# based on debian:jessie
FROM php:7.4-fpm-alpine

# install depedencies
RUN apk add --no-cache \
    zip libzip-dev \
    oniguruma-dev \
    postgresql-dev

# install php extensions
RUN docker-php-ext-configure opcache --enable-opcache \
    && docker-php-ext-install \
        zip \
        bcmath \
        pdo_pgsql \
        sockets \
        opcache
    
COPY php.ini /usr/local/etc/php/
