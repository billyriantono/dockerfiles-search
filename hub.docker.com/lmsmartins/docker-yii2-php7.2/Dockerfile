FROM php:7.2-apache
RUN apt-get update -y && apt-get install -y libpng-dev vim
RUN apt-get update && \
     apt-get install -y \
         zlib1g-dev
RUN docker-php-ext-install pdo pdo_mysql
RUN a2enmod rewrite