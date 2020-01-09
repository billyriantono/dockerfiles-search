FROM php:7.2.0-apache

RUN apt-get update && apt-get install -y git libpng-dev libfreetype6-dev libjpeg62-turbo-dev && \
    docker-php-ext-configure pdo_mysql --with-pdo-mysql=mysqlnd && \
    docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ && \
    docker-php-ext-install pdo_mysql && docker-php-ext-install -j$(nproc) gd 

RUN usermod -u 1000 www-data && groupmod -g 1000 www-data
RUN sed -i -e "s/html/html\/web/g" /etc/apache2/sites-enabled/000-default.conf
RUN a2enmod rewrite
