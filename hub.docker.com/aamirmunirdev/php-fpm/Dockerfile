#https://github.com/docker-library/php/tree/master/7.1/apache
FROM php:7.1-apache

RUN pecl install xdebug

RUN docker-php-ext-enable xdebug

RUN echo "xdebug.remote_enable=1" >> /usr/local/etc/php/php.ini

# Install Composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer
#RUN composer --version

#Install git & Zip / unzip
#RUN apt-get update && apt-get install -y \
#  git \
#  zip \
#  unzip

#RUN a2enmod rewrite && service apache2 restart