FROM php:latest

RUN apt-get update
RUN apt-get upgrade -y
RUN apt-get install libpq-dev -y
RUN docker-php-ext-install pdo pdo_pgsql