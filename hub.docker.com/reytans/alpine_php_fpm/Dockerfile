FROM	php:7.1-fpm-alpine

RUN apk update \
  && apk add libmcrypt-dev iputils \
  && docker-php-ext-install mcrypt mysqli pdo pdo_mysql \
  && rm /var/cache/apk/*
