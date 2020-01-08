FROM jakzal/phpqa:alpine

RUN apk update \
    && apk add --no-cache --virtual .phpize-deps $PHPIZE_DEPS \
    && pecl install xdebug-2.6.0 \
    && docker-php-ext-enable xdebug \
    && pecl clear-cache \
    && apk del .phpize-deps
    