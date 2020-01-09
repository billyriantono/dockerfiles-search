FROM php:fpm-alpine

RUN apk add --no-cache --update \
    libxml2-dev \
    && docker-php-ext-install -j$(nproc) bcmath soap