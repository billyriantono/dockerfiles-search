FROM php:7.1-apache

ADD ./php.ini /usr/local/etc/php

# Install vi
RUN apt-get update \
    && apt-get install -y vim


# Install MCrypt
RUN apt-get update \
    && apt-get install -y libmcrypt-dev \
	unzip \
    git \
    libpng-dev \
    && docker-php-ext-install mcrypt \
	&& docker-php-ext-install mysqli pdo pdo_mysql

# Install GD-lib
RUN docker-php-ext-install gd

# Install Intl
RUN apt-get update \
    && apt-get install -y libicu-dev \
	libxml2-dev \
    && docker-php-ext-install intl \
    && docker-php-ext-install soap

RUN apt-get update \
    && apt-get install -y zlib1g-dev \
    && docker-php-ext-install zip
	

	
RUN curl -sS https://getcomposer.org/installer | php \
    && mv composer.phar /usr/local/bin/composer
	
RUN docker-php-ext-install mbstring

# Install GD
RUN apt-get install -y libfreetype6-dev libjpeg62-turbo-dev
RUN docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/
RUN docker-php-ext-install gd

ENV PHP_TIMEZONE Europe/Berlin

RUN a2enmod rewrite

RUN service apache2 restart

COPY ./apache.conf /etc/apache2/sites-available/


RUN a2ensite apache.conf



