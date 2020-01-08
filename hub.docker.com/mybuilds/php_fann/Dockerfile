FROM php:7.0-apache

MAINTAINER stephanelaverdure <stephanelaverdure@hotmail.fr>

# Change user et group id
RUN usermod -u 1000 www-data

# Update & install libfann
RUN apt-get update && apt-get install -y libfann-dev

# Install fann & activate it (don't know if that part actualy works...).
RUN pecl install fann && docker-php-ext-enable fann

# Enable fann extension
ADD fann.ini /usr/local/etc/php/conf.d/

# Start apache2
CMD ["apache2-foreground"]
