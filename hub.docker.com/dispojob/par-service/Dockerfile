FROM php:7.3-fpm

RUN apt-get update && apt-get install -y \
        make \
        libxml2-dev \
        libpq-dev \
        openssl \
        git \
        unzip

RUN docker-php-ext-install xml intl mbstring bcmath sockets