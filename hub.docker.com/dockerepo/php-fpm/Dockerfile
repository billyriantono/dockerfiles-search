FROM alpine:3.4

MAINTAINER Vincent Composieux <vincent.composieux@gmail.com>

RUN apk add --update \
    php5-fpm \
    php5-apcu \
    php5-curl \
    php5-gd \
    php5-iconv \
    php5-imagick \
    php5-json \
    php5-intl \
    php5-mcrypt \
    php5-mysql \
    php5-opcache \
    php5-openssl \
    php5-pdo \
    php5-pdo_mysql \
    php5-mysqli \
    php5-xml \
    php5-zlib \
    php5-dom \
    php5-ctype

RUN rm -rf /var/cache/apk/* && rm -rf /tmp/*

RUN addgroup -g 82 -S www-data \
	&& adduser -u 82 -D -S -G www-data www-data

CMD ["php-fpm", "-F"]

EXPOSE 9000
