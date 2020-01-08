FROM php:5-fpm-alpine

RUN apk add --update ca-certificates zlib-dev libpng-dev libressl-dev libmcrypt-dev git postgresql-dev && rm -rf /var/cache/apk/* \
    && docker-php-ext-install gd pcntl mcrypt mysql mysqli pdo pdo_mysql pgsql pdo_pgsql zip calendar

EXPOSE 9000
CMD ["php-fpm"]
