FROM php:5.6-apache

RUN a2enmod rewrite

RUN apt-get update && apt-get install -y \
		vim \
		mysql-client \
		#mysql-server \
		subversion \
		#mysqli \
		curl \
		libcurl4-gnutls-dev \
		libmcrypt-dev \
--no-install-recommends && rm -r /var/lib/apt/lists/*

RUN docker-php-ext-install pdo pdo_mysql curl sockets

#COPY config/php.ini /usr/local/etc/php/php.ini

#required for the 3des encryption
RUN docker-php-ext-configure mcrypt
RUN docker-php-ext-install mcrypt

# Make port 80 available to the world outside this container
EXPOSE 80
EXPOSE 143
EXPOSE 993
EXPOSE 25