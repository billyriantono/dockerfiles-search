FROM php:5.6.2-apache
MAINTAINER Elber Ribeiro <elber@dynaum.com>

# PHP Extension: Zip
RUN pecl install zip
RUN echo "extension=zip.so" >> /usr/local/lib/php.ini

# Set environmental variables
ENV COMPOSER_HOME /root/composer

# Install Composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer --version=1.0.0-alpha8

# Display Composer version information
RUN composer --version

# PHP Extensions
RUN apt-get update && \
    apt-get -y install \
    php5-mcrypt \
    php5-intl

RUN php5enmod mcrypt
