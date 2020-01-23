FROM php:apache

ARG PACKAGES="git"

RUN apt-get update && apt-get install -y
RUN apt-get install -y $PACKAGES

RUN apt-get install -y libpq-dev && docker-php-ext-install pdo pdo_pgsql
RUN apt-get install -y mysql-client && docker-php-ext-install pdo_mysql

RUN git clone https://github.com/vrana/adminer .
