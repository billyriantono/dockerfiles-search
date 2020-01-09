FROM php:5-apache
MAINTAINER Mike Petersen <mike@odania-it.de>

WORKDIR /var/www/html

RUN apt-get update \
	&& apt-get -y install libpng-dev \
	&& apt-get clean
RUN docker-php-ext-install gd mysqli

COPY dist /
RUN tar -xvzf *.tar.gz \
	&& rm *.tar.gz \
	&& chown -R www-data:www-data /var/www/html

ENTRYPOINT ["entrypoint.sh"]
