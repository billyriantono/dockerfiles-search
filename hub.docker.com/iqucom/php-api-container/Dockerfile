FROM php:5-fpm

MAINTAINER mauricio.van.der.maesen@iqu.com

# Dependencies
RUN apt-get update \
    && apt-get upgrade -y \
    && apt-get autoremove -y \
    && apt-get install -y git wget nano libmcrypt-dev libpng12-dev libjpeg-dev libpq-dev mysql-client curl phing php-gettext php-soap \
    && rm -rf /var/lib/apt/lists/* \
    && docker-php-ext-configure gd --with-png-dir=/usr --with-jpeg-dir=/usr --with-gettext\
    && docker-php-ext-install mcrypt gd mbstring pdo pdo_mysql zip gettext \
    && rm -rf /tmp/pear

RUN php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');"
RUN php -r "if (hash_file('SHA384', 'composer-setup.php') === '669656bab3166a7aff8a7506b8cb2d1c292f042046c5a994c43155c0be6190fa0355160742ab2e1c88d40d5be660b410') { echo 'Installer verified'; } else { echo 'Installer corrupt'; unlink('composer-setup.php'); } echo PHP_EOL;"
RUN php composer-setup.php
RUN php -r "unlink('composer-setup.php');"
RUN mv composer.phar /usr/local/bin/composer

RUN git clone https://github.com/mongodb/mongo-php-driver-legacy.git \
	&& cd mongo-php-driver-legacy \
	&& phpize \
	&& ./configure \
	&& make \
	&& make install

# PHP configuration files
RUN echo "extension=mongo.so" > /usr/local/etc/php/conf.d/mongo.ini
RUN echo "extension=soap.so" > /usr/local/etc/php/conf.d/soap.ini

# open port
EXPOSE 9000
