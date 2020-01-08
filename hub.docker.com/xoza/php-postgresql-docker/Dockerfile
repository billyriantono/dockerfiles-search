FROM php:7.2-cli-alpine3.7

RUN apk update \
    && apk upgrade \
    && apk add --no-cache $PHPIZE_DEPS \
    && apk add php7-curl postgresql-libs postgresql-dev \
    && docker-php-ext-install pgsql pdo_pgsql \
    && apk del postgresql-dev
