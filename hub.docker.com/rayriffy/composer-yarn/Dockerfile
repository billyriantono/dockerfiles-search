FROM php:7.2.6-fpm-alpine3.7

RUN apk update && \
    apk --no-cache add \ 
        curl \
        curl-dev \
        libxml2 \
        libxml2-dev && \
    docker-php-ext-install \
        pdo \
        pdo_mysql \
        curl \
        mbstring \
        xml \
        xmlwriter \
        tokenizer \
        ctype \
        json && \
    curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/bin --filename=composer && \
    apk update && \
    apk --no-cache add \
        tar \
        nodejs \
        yarn \
        alpine-sdk \
        bash \
        lcms2-dev \
        libpng-dev \
        gcc \
        g++ \
        make \
        autoconf \
        automake && \
    rm -rf /var/cache/apk/*