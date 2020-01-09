FROM composer:latest

RUN apk --no-cache add bash git lftp

RUN apk --no-cache add postgresql-dev
RUN docker-php-ext-install pgsql
RUN docker-php-ext-install pdo pdo_pgsql

