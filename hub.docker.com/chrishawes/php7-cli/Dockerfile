FROM php:7-zts-alpine

ENV PHPREDIS_VERSION 3.0.0
ENV PTHREADS_URL https://github.com/krakjoe/pthreads/archive/master.tar.gz

RUN mkdir -p /usr/src/php/ext/redis \
    && curl -L https://github.com/phpredis/phpredis/archive/$PHPREDIS_VERSION.tar.gz | tar xvz -C /usr/src/php/ext/redis --strip 1 \
    && echo 'redis' >> /usr/src/php-available-exts \
    && docker-php-ext-install redis

RUN mkdir -p /usr/src/php/ext/pthreads \
    && curl -L $PTHREADS_URL | tar xvz -C /usr/src/php/ext/pthreads --strip 1 \
    && echo 'pthreads' >> /usr/src/php-available-exts \
    && docker-php-ext-install pthreads

RUN apk add --update ca-certificates zlib-dev libpng-dev libressl-dev libsodium-dev git postgresql-dev && rm -rf /var/cache/apk/* \
    && docker-php-ext-install gd pcntl mysqli pdo pdo_mysql pgsql sodium pdo_pgsql zip bcmath sockets posix shmop


CMD ["php"]
