FROM php:7-apache

RUN apt-get update \
	
	&& apt-get install -y \
		libmcrypt-dev \
		libjpeg62-turbo-dev \
		libpng12-dev \
		libfreetype6-dev \
		libxml2-dev \
		libicu-dev \	
	&& rm -rf /var/lib/apt/lists/* \
	&& docker-php-ext-configure gd --with-png-dir=/usr --with-jpeg-dir=/usr \
	&& docker-php-ext-install iconv intl mcrypt opcache pdo pdo_mysql mysqli mbstring soap gd zip

RUN a2enmod rewrite
RUN chown -R www-data:www-data /var/www/html/

VOLUME /var/www/html

# CMD ["apache2-foreground"]
