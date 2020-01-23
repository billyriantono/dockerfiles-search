FROM php:7.3-apache

MAINTAINER Giambra Domenico <zorinik@gmail.com>

RUN apt-get update && apt-get -y upgrade && apt-get install -y ntp zip git curl \
	&& docker-php-ext-install -j$(nproc) opcache pdo_mysql mbstring \
	&& curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer \
	&& echo Europe/Rome > /etc/timezone && ln -sf /usr/share/zoneinfo/Europe/Rome /etc/localtime && dpkg-reconfigure -f noninteractive tzdata

RUN  printf "date.timezone = Europe/Rome" > /usr/local/etc/php/php.ini

RUN a2enmod rewrite

EXPOSE 80

COPY wait-for-it.sh /var/www/wait-for-it.sh
COPY entrypoint.sh /var/www/entrypoint.sh
COPY app /var/www/html
COPY migrations /var/www/migrations

RUN chown -R www-data:www-data /var/www && chmod +x /var/www/entrypoint.sh && chmod +x /var/www/wait-for-it.sh

WORKDIR /var/www/html
RUN composer install

WORKDIR /var/www

ENTRYPOINT ["docker-php-entrypoint", "/var/www/entrypoint.sh"]