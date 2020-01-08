FROM php:7.3-fpm-alpine

RUN apk update && apk add --no-cache $PHPIZE_DEPS
RUN apk add --no-cache freetype libpng libjpeg-turbo freetype-dev libpng-dev libjpeg-turbo-dev zlib-dev libzip-dev
RUN docker-php-ext-install mysqli gd zip
RUN docker-php-ext-enable mysqli
RUN chown -R www-data:www-data /var/www
