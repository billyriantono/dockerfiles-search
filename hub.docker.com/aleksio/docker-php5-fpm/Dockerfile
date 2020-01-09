FROM debian:jessie

MAINTAINER Alexey V. Grebenshchikov "mi.aleksio@gmail.com"

RUN apt-get update \
&& apt-get install \ 
--no-install-recommends \
--no-install-suggests \
-y \
php5-cli \
php5-fpm \
php5-apcu \
php5-curl \
php5-gd \
php5-json \
php5-mcrypt \
php5-pgsql \
php5-sqlite \
php5-readline \
php5-xsl

COPY deb /deb

RUN dpkg -iR /deb/jessie

EXPOSE 9000
CMD ["php5-fpm", "-F"]

