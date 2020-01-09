FROM alpine:3.8
MAINTAINER Shamaru Primera <shamaru001@gmail.com>
LABEL maintainer="shamaru001@gmail.com"

RUN apk upgrade --update-cache && \
    apk add curl ca-certificates && \
    apk update && \
    apk add  php7 \
    php7-phar \
    php7-json \
    php7-openssl \
    php7-dom \
    php7-mysqlnd \
    php7-mysqli \
    php7-posix \
    php7-pcntl \
    php7-pdo \
    php7-pdo_pgsql \
    php7-pdo_sqlite \
    php7-pdo_mysql \
    php7-common \
    php7-fpm \
    php7-bcmath \
    php7-zip \
    php7-bz2 \
    php7-curl \
    php7-gd \
    php7-intl \
    php7-sqlite3 \
    php7-ctype \
    php7-tidy \
    php7-pgsql \
    php7-xml \
    php7-mbstring \
    php7-session \
    php7-zlib \
    php7-opcache \
    php7-soap \
    php7-xdebug \
    php7-imagick \
    php7-exif \
    php7-tokenizer \
    php7-xmlwriter \
    php7-fileinfo \
    php7-simplexml \
    php7-xmlreader \
    php7-iconv \
    nodejs \
    npm \
    git \
    curl;
RUN    rm -rf /var/cache/apk/*
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer
WORKDIR /var/www/

EXPOSE 80
EXPOSE 443
