FROM php:7-fpm-alpine

ENV PHPREDIS_VERSION 3.0.0

RUN mkdir -p /usr/src/php/ext/redis \
    && curl -L https://github.com/phpredis/phpredis/archive/$PHPREDIS_VERSION.tar.gz | tar xvz -C /usr/src/php/ext/redis --strip 1 \
    && echo 'redis' >> /usr/src/php-available-exts \
    && docker-php-ext-install redis \
    && apk add --update ca-certificates zlib-dev libpng-dev libressl-dev libsodium-dev git postgresql-dev autoconf gcc g++ make \
    && pecl install apcu-5.1.9 \
    && docker-php-ext-enable apcu \
    && docker-php-ext-install gd pcntl mysqli pdo pdo_mysql pgsql sodium pdo_pgsql zip bcmath sockets posix shmop \
    && rm -rf /var/cache/apk/* \
    && rm -rf /tmp/pear

EXPOSE 9000

CMD ["php-fpm"]
