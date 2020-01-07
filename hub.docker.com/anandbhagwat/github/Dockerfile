FROM php:apache
RUN apt-get update 
RUN apt-get --yes  install  nano
RUN apt-get --yes  install  curl
RUN apt-get --yes install iputils-ping
RUN apt-get --yes install vim
RUN apt-get --yes install net-tools
RUN docker-php-ext-install mysqli
#/usr/local/etc/php
WORKDIR /var/www/html
COPY . .
EXPOSE 80

