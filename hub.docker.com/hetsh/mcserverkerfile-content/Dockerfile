FROM php:7.0.25-apache-jessie

MAINTAINER Luis Herrera <luis.herrera.ec@gmail.com>

RUN apt-get update
RUN apt-get install -y  nano
RUN a2enmod rewrite

COPY apache2.conf /etc/apache2/
COPY index.php /var/www/html/

EXPOSE 80 443

