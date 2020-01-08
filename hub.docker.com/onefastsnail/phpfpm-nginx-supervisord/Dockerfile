FROM php:7.2-fpm-alpine

LABEL maintainer="Paul Stewart"

RUN apk --no-cache add nginx supervisor

RUN docker-php-ext-install mysqli
