FROM php:7.3.6-apache

RUN apt-get update \
    && apt-get install -y git \
    && apt-get install -y nano \
    && apt-get install -y ntp \
    && apt-get install -y mysql-client curl \
    && docker-php-ext-install pdo pdo_mysql mysqli calendar \
    && apt-get clean \
    && rm -rf /var/cache/apt/archives

RUN echo "TZ=Asia/Jakarta" >> /etc/environment

RUN a2enmod rewrite

COPY ./ini/php.ini "$PHP_INI_DIR/"

RUN chmod -R 775 /var/www/html/

COPY . /var/www/html/
