FROM php:7.2-cli

LABEL maintainer="Dan Streeter <dan@danstreeter.co.uk>"

RUN pecl install xdebug-2.6.0 \
    && docker-php-ext-enable xdebug

COPY ./xdebug.ini /usr/local/etc/php/conf.d/xdebug.ini