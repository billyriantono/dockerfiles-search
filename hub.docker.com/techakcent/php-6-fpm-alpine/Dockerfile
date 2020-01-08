FROM php:5-fpm-alpine
RUN docker-php-ext-install mysqli \
    && docker-php-ext-install mysql

COPY uploads.ini /usr/local/etc/php/conf.d/uploads.ini