FROM php:7.2.4-fpm-alpine

RUN set -x \
    && apk --update add --no-cache postgresql-dev php7-pgsql \
    && docker-php-ext-install pgsql \
    && docker-php-ext-configure pgsql -with-pgsql=/usr/local/pgsql \
    && kill -USR2 1

EXPOSE 80
EXPOSE 443
