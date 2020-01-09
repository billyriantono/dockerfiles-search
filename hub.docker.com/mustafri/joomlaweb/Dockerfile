FROM php:5.6.31-apache
RUN docker-php-source extract \
&& apt-get update \
&& apt-get install php5-mysql vim libmcrypt-dev -y \
&& docker-php-ext-install mysqli pdo pdo_mysql mcrypt
