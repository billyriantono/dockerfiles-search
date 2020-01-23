FROM php:fpm

RUN printf 'date.timezone = "America/Sao_Paulo"\nmemory_limit = 256M\n' > /usr/local/etc/php/php.ini

RUN apt update && apt install -y git-core zlib1g-dev

RUN docker-php-ext-install -j$(nproc) pdo_mysql zip

COPY ./composer_install.sh .
RUN sh ./composer_install.sh

WORKDIR /var/www
