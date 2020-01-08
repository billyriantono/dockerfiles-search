FROM php:7.2-fpm-alpine

RUN apk add --no-cache --virtual .builddeps build-base musl-dev autoconf git \
       \
    && apk add --no-cache --virtual .phpextdeps libpng-dev jpeg-dev freetype-dev libmcrypt-dev icu-dev \
    && docker-php-ext-configure gd --with-freetype-dir=/usr/include/freetype --with-jpeg-dir=/usr/include --with-png-dir=/usr/include \
    && docker-php-ext-install gd pdo_mysql zip intl \
       \
    && git clone https://github.com/xdebug/xdebug.git \
    && cd xdebug && ./rebuild.sh && cd .. && rm -rf xdebug \
    && docker-php-ext-enable xdebug \
    && echo 'xdebug.remote_enable=On' >> /usr/local/etc/php/conf.d/tuning.ini \
       \
    && strip /usr/local/lib/php/extensions/*/*.so \
    && apk del .builddeps && rm -rf /tmp/* \
    && php -v
