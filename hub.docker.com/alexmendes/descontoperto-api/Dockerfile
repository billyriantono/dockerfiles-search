FROM php:7.2-apache

#RUN apt-add-repository ppa:ondrej/php
RUN apt-get update
RUN apt-get install git zip unzip -y

RUN docker-php-ext-install pdo pdo_mysql

RUN a2enmod headers
RUN a2enmod rewrite

RUN sed -i 's/\/var\/www\/html/\/var\/www\/html\/public/g' /etc/apache2/sites-enabled/000-default.conf

RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

COPY . /var/www/html/
WORKDIR /var/www/html

RUN php /usr/local/bin/composer install

RUN chmod -R 777 storage/ 
RUN chmod -R 777 bootstrap/cache/

RUN php artisan key:generate

EXPOSE 80
#RUN ["apache2-foreground"]