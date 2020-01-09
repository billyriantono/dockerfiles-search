FROM php:7.1

LABEL maintainer="christian.wreden@googlemail.com"

WORKDIR "/app"

RUN  apt-get update -yqq \
     && apt-get install git zlib1g-dev -yqq \
     && docker-php-ext-install zip

RUN curl -sS https://getcomposer.org/installer | php \
    && mv composer.phar /usr/local/bin/composer

