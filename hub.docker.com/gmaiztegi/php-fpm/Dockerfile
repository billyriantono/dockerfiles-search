FROM alpine:3.8
MAINTAINER Gorka Maiztegi <gmaiztegi@gmail.com>

RUN set -x \
    && apk upgrade --no-cache \
    && apk --no-cache add ca-certificates curl \
    && curl https://php.codecasts.rocks/php-alpine.rsa.pub -o /etc/apk/keys/php-alpine.rsa.pub \
    && echo "@php https://php.codecasts.rocks/v3.8/php-7.2" >> /etc/apk/repositories \
    && apk add --no-cache \
    php@php \
    php-fpm@php \
    php-apcu@php \
    php-bcmath@php \
    php-ctype@php \
    php-curl@php \
    php-exif@php \
    php-gd@php \
    php-iconv@php \
    php-intl@php \
    php-json@php \
    php-mbstring@php \
    php-opcache@php \
    php-openssl@php \
    php-pcntl@php \
    php-pdo@php \
    php-mysqlnd@php \
    php-pdo_mysql@php \
    php-pdo_pgsql@php \
    php-phar@php \
    php-posix@php \
    php-session@php \
    php-xml@php \
    php-xmlreader@php \
    php-xsl@php \
    php-zip@php \
    php-zlib@php \
    php-dom@php \
    php-redis@php \
    php-sodium@php \
    ssmtp \
    && apk add --no-cache --repository http://dl-3.alpinelinux.org/alpine/edge/testing gnu-libiconv \
    && rm -rf /var/cache/apk/* \
    && echo "UTC" > /etc/timezone \
    && addgroup -S www-data \
    && adduser -D -S -h /var/cache/php -s /sbin/nologin -G www-data www-data \
    && mkdir /app

ENV LD_PRELOAD /usr/lib/preloadable_libiconv.so

COPY php.ini /etc/php7/php.ini
COPY www.conf /etc/php7/php-fpm.d/www.conf
COPY zz-www.conf /etc/php7/php-fpm.d/zz-www.conf

EXPOSE 9000

WORKDIR /app

CMD ["php-fpm7", "-F"]
