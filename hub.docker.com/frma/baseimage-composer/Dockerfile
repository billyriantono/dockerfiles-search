FROM php:5.6-apache
MAINTAINER Firmansyah Adiputra <frm.adiputra@gmail.com>

RUN apt-get update \
    && apt-get install -y \
    	gawk \
    	git \
    	libmcrypt-dev \
    	libzip-dev \
    && rm -rf /var/lib/apt/lists/*

# Install PHP extension
RUN docker-php-ext-install \
	iconv \
	mbstring \
	mcrypt \
	pdo \
	zip

# Install Composer
RUN curl -sS https://getcomposer.org/installer | php -- --version=1.0.0-alpha11 \
 && mv composer.phar /usr/local/bin/composer
