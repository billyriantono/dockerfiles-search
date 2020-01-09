FROM php:7.1-fpm-alpine3.10

RUN apk --no-cache add pcre-dev ${PHPIZE_DEPS} \
    && pecl install redis-4.0.1 \
    && pecl install xdebug-2.6.0 \
    && pecl install mongodb-1.6.0 \
    && docker-php-ext-enable redis xdebug mongodb \
    && apk del pcre-dev ${PHPIZE_DEPS}
