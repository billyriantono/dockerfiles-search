FROM 4xxi/php:7.2.2-fpm-alpine3.7

RUN apk upgrade --update && apk add \
autoconf \
gcc \
libc-dev \
openssl-dev \
make \
pcre-dev

# install mongodb ext
RUN pecl install mongodb \
    && docker-php-ext-enable mongodb
RUN ln -s $(php-config --extension-dir) /usr/local/lib/php/extensions/no-debug-non-zts
RUN apk del --purge gcc autoconf make pcre-dev
