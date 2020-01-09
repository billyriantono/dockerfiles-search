FROM php:7.2-zts-alpine3.8

LABEL maintainer="PixartPrinting Magenta Team"

ENV PATH="/var/www/vendor/bin:${PATH}"

USER root

RUN ln -snf /usr/share/zoneinfo/Europe/Rome /etc/localtime && \
    echo Europe/Rome > /etc/timezone

RUN apk add --update build-base \
                     coreutils \
                     ca-certificates \
                     curl \
                     freetype-dev \
                     git \
                     icu-dev \
                     inotify-tools \
                     libjpeg-turbo-dev \
                     libpng-dev \
                     libxml2-dev \
                     libmcrypt-dev \
                     musl-dev \
                     openldap-dev \
                     openssh \
                     supervisor \
                     zip

RUN docker-php-ext-install bcmath ctype gd ldap intl json mysqli pdo pdo_mysql soap zip
RUN apk add --update --no-cache --virtual autoconf gcc g++ make
RUN rm -fr /var/cache/apk/*
RUN pecl install swoole
RUN docker-php-ext-enable swoole

COPY cert.crt /tmp/cert.crt
RUN cp /tmp/cert.crt /usr/local/share/ca-certificates/ && update-ca-certificates

RUN curl --fail -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer
RUN composer global require hirak/prestissimo

COPY ./conf/php.ini /usr/local/etc/php/

RUN rm -rf /tmp/*

WORKDIR /var/www
