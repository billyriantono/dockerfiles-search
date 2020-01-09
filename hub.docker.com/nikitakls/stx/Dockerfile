# Базовый образ с nginx и php
# alpine выше 3.8 не поддерживается т.к. нельзя установить unoconv pdftk т.к. нет
# библиотеки для 3.9 и выше
FROM php:7.2-fpm-alpine3.8

ENV UNO_URL https://raw.githubusercontent.com/dagwieers/unoconv/master/unoconv

RUN apk update && apk upgrade && apk add bash mc php7-zmq \
        curl \
        pdftk \
        busybox-suid \
        util-linux \
        libreoffice-common \
        libreoffice-writer \
        ttf-droid-nonlatin \
        ttf-droid \
        ttf-dejavu \
        ttf-freefont \
        ttf-liberation \
        libzip-dev \
        libxml2-dev \
        libpng-dev libpng libjpeg-turbo freetype-dev libjpeg-turbo-dev \
        icu-dev \
    && curl -Ls $UNO_URL -o /usr/bin/unoconv \
    && sed -i 's#!/usr/bin/env python#!/usr/bin/env python3#g' /usr/bin/unoconv \
    && chmod +x /usr/bin/unoconv \
    && apk del curl \
    && rm -rf /var/cache/apk/* \
    && ln -s  /usr/lib/php7/modules/zmq.so /usr/local/lib/php/extensions/no-debug-non-zts-20170718/zmq.so \
    && docker-php-ext-enable zmq \
    && docker-php-ext-configure gd \
        --with-gd \
        --with-freetype-dir=/usr/include/ \
        --with-png-dir=/usr/include/ \
        --with-jpeg-dir=/usr/include/ \
    && docker-php-ext-install iconv pdo_mysql json intl opcache xml dom zip gd \
    && docker-php-source delete \
    && apk del --no-cache freetype-dev libpng-dev libjpeg-turbo-dev icu-dev libxml2-dev libzip-dev

WORKDIR "/var/www/app"

ADD scripts/start.sh /start.sh
ADD scripts/crontab /home/crontab
ADD conf/php-fpm.conf /usr/local/etc/php-fpm.d/www.conf
ADD conf/php.ini /usr/local/etc/php/php.ini

RUN chmod 755 /start.sh && rm /etc/crontabs/root

CMD ["/start.sh"]
