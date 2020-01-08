FROM php:5-fpm

RUN docker-php-ext-install -j$(nproc) pdo_mysql
COPY php.ini /usr/local/etc/php/php.ini