FROM php:7

RUN apt-get update && apt-get install -y \
        libyaml-dev;

RUN pecl install yaml && docker-php-ext-enable yaml
