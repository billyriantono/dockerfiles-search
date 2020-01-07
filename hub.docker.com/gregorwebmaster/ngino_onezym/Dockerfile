FROM php:7.3-fpm-alpine3.8

RUN apk update && apk upgrade

# Install modules
RUN apk add php7-common \
    php7-opcache \
    php7-openssl \
    php7-session \
    php7-sockets \
    php7-curl \
    php7-json \
    php7-yaml \
    php7-xml \
    php7-simplexml \
    php7-mysqli \
    php7-pdo_mysql \
    php7-pdo \
    php7-pdo_sqlite \
    php7-redis \
    php7-pear \
    php7-phar \
    php7-gd \
    php7-iconv \
    php7-mbstring \
    php7-tokenizer \
    php7-mcrypt \
    php7-ctype \
    php7-zlib \
    php7-zip
    
# cleare installation
RUN rm -rf /var/cache/apk/*

# set workdir
RUN mkdir /workdir
WORKDIR /workdir
