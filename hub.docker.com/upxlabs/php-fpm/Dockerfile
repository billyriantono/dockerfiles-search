FROM php:7.2-fpm-alpine

MAINTAINER UPX Technologies "labs@upx.com"

RUN apk --no-cache --update add wget \
        curl \
        git \
        vim \
        grep \
        gmp-dev \
        freetype-dev \
        libxpm-dev \
        libwebp-dev \
        libjpeg-turbo-dev \
        libjpeg \
        bzip2-dev \
        openssl-dev \
        krb5-dev \
        libxml2-dev \
        build-base \
        tar \
        make \
        autoconf \
        g++ \
        wget && \
    docker-php-source extract && \
    pecl install xdebug mongodb && \
    docker-php-ext-install mysqli \
        pdo \
        pdo_mysql \
        mbstring \
        tokenizer \
        iconv \
        zip \
        gmp \
        bcmath && \
    docker-php-source delete

RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer
ENV COMPOSER_ALLOW_SUPERUSER 1

COPY xdebug /usr/local/bin/xdebug
RUN chmod +x /usr/local/bin/xdebug

WORKDIR /var/www/app
