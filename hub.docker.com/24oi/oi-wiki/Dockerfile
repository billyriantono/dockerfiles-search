FROM 1maa/alpine:3.5

RUN apk add --no-cache \
    libsodium \
    php7 \
    php7-apcu \
    php7-bcmath \
    php7-bz2 \
    php7-ctype \
    php7-curl \
    php7-exif \
    php7-gd \
    php7-iconv \
    php7-intl \
    php7-json \
    php7-mbstring \
    php7-opcache \
    php7-openssl \
    php7-pcntl \
    php7-pdo_mysql \
    php7-pdo_pgsql \
    php7-pdo_sqlite \
    php7-phar \
    php7-posix \
    php7-session \
    php7-soap \
    php7-xml \
    php7-xsl \
    php7-zip \
    php7-zlib \
 && ln -s /usr/bin/php7 /usr/bin/php

COPY common_settings.ini /etc/php7/conf.d/common_settings.ini
COPY 70/*.ini            /etc/php7/conf.d/
COPY 70/*.so             /usr/lib/php7/modules/
