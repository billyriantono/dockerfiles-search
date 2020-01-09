FROM php:7.3-fpm-alpine3.10

LABEL maintainer="Nextar Developers <dev@nextar.com.br>"
LABEL version="0.0.1"

RUN apk add unzip zip git sed \
    && docker-php-ext-install pdo_mysql opcache sockets \
    && curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer \
    && composer global require hirak/prestissimo
