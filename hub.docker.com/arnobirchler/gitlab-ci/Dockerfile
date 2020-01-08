FROM php:7.2-fpm

RUN apt-get update && \
	apt-get install -y --no-install-recommends \
	git \
	curl \
	libzip-dev

#Install Xdebug
RUN pecl install xdebug && docker-php-ext-enable xdebug

#Install ZIP
RUN pecl install zip && docker-php-ext-enable zip

#Install composer
RUN php -r "readfile('http://getcomposer.org/installer');" | php -- --install-dir=/usr/bin/ --filename=composer \
    && rm -rf /var/lib/apt/lists/*

#RUN curl -sS https://getcomposer.org/installer | php
#RUN mv composer phar /usr/local/bin/composer

