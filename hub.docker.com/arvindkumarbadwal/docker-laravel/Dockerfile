# Laravel 5.7 Dockerfile
FROM php:7.2-fpm

LABEL maintainer="arvindkumar.b@hotmail.com"
LABEL version="1.0"
LABEL description="This is an simple laravel 5.7 dockerfile"

RUN apt-get update -y
RUN apt-get install -y libmcrypt-dev libxml2-dev openssl curl zip unzip
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

COPY ./src /var/www/html

WORKDIR /var/www/html

RUN composer install
RUN cp .env.example .env
RUN php artisan key:generate
RUN chmod 777 -R storage/ bootstrap/cache

CMD php artisan serve --host=0.0.0.0 --port=8333

EXPOSE 8333