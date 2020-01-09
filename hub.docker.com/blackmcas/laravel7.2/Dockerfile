FROM php:7.2-fpm
RUN apt-get update && apt-get install -y unzip zip ssh rsync git git-ftp libzip-dev libgmp-dev
RUN docker-php-ext-install zip gmp bcmath
RUN docker-php-ext-enable zip gmp bcmath
RUN pecl install xdebug
RUN docker-php-ext-enable xdebug