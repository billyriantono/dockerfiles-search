#
#--------------------------------------------------------------------------
# Image Setup
#--------------------------------------------------------------------------
#

FROM php:7.2-apache
MAINTAINER Ximil Technologies <info@ximil.co>

COPY config/php.ini /usr/local/etc/php/
COPY app /var/www/html

RUN apt-get update && \
    apt-get install -y imagemagick vim curl git

COPY config/policy.xml /etc/ImageMagick-6/policy.xml

RUN docker-php-ext-install fileinfo
RUN a2enmod rewrite

RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

RUN composer update --working-dir=/var/www/html
RUN chown -R www-data:www-data /var/www/html
WORKDIR /var/www/html
