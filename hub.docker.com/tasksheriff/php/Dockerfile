FROM php:7.2-cli

RUN apt-get update && apt-get install -y git build-essential unzip libwebp-dev libpng-dev libjpeg-dev libz-dev libxpm-dev libzip-dev
RUN docker-php-ext-configure gd
RUN docker-php-ext-configure zip
RUN docker-php-ext-install gd zip
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer
