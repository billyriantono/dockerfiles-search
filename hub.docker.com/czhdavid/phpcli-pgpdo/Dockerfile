FROM php:7.1.14-cli

RUN apt-get update \
  && apt-get install -y libpq-dev && docker-php-ext-install pdo pdo_pgsql

EXPOSE 5432:5432
