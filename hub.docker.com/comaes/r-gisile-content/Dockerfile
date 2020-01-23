FROM php:7.0-apache
MAINTAINER Johannes Berthel <j.berthel@codeblick.de>


RUN apt-get update


# PHP
# install opcache
RUN docker-php-ext-install opcache

# install APCu
RUN pecl install apcu
RUN echo "extension=apcu.so" > /usr/local/etc/php/conf.d/apcu.ini

# install GD
RUN apt-get install -y libfreetype6-dev libjpeg62-turbo-dev libpng12-dev
RUN docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/
RUN docker-php-ext-install gd

# install pdo
RUN docker-php-ext-install pdo_mysql

# install mcrypt
RUN apt-get install -y libmcrypt-dev
RUN docker-php-ext-install mcrypt

# install zip
RUN docker-php-ext-install zip

# install ioncube
COPY ./assets/ioncube_loader_lin_7.0.so /usr/local/ioncube/
RUN echo "zend_extension=/usr/local/ioncube/ioncube_loader_lin_7.0.so" > /usr/local/etc/php/conf.d/00-ioncube.ini

# copy php ini
COPY ./assets/php.ini /usr/local/etc/php/

# APACHE
# enable mod_rewrite
RUN a2enmod rewrite
RUN sed -i 's/www-data:x:33:33/www-data:x:1000:1000/g' /etc/passwd


RUN rm -rf /var/lib/apt/lists/*