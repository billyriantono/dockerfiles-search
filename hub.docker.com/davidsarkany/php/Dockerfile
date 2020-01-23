FROM php:7-fpm-alpine
RUN docker-php-ext-install \
        pdo_mysql \
        opcache

COPY --from=composer:latest /usr/bin/composer /usr/bin/composer
