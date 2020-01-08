# Download base
FROM php:5.6-apache

MAINTAINER pyarza

# Instalar PDO POSTGRESQL
RUN apt-get update
RUN apt-get install -y libpq-dev
RUN docker-php-ext-install pdo pdo_pgsql
