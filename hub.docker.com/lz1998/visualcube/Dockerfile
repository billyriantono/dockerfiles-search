FROM php:7.2-apache
RUN apt-get update \
	&& apt-get install imagemagick -y
COPY visualcube/ /var/www/html/
EXPOSE 80