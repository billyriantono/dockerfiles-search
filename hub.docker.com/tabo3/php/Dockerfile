FROM php:7.0-fpm

RUN apt-get update && apt-get -y install git zlib1g-dev

RUN docker-php-ext-install \
        pdo_mysql \
        zip

RUN curl -sS https://getcomposer.org/installer | php \
    && mv composer.phar /usr/local/bin/composer
