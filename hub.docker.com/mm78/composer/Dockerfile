FROM php

RUN apt-get update -y && apt-get upgrade -y
RUN apt-get update -y && apt-get install -y curl zip zlib1g-dev libzip-dev

RUN docker-php-ext-install zip

RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer