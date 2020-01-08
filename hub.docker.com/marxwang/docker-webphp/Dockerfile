FROM ubuntu:latest
MAINTAINER marxwang

# Install packages
ENV DEBIAN_FRONTEND noninteractive
RUN apt-get update && \
  apt-get -y install supervisor git apache2 libapache2-mod-php5 mysql-server php5-mysql pwgen php-apc php5-mcrypt curl && \
echo "ServerName localhost" >> /etc/apache2/apache2.conf && \
echo "deb http://repo.suhosin.org/ ubuntu-trusty main" > /etc/apt/sources.list.d/suhosin.list && \
 curl -s https://sektioneins.de/files/repository.asc  | apt-key add -
#add php5-suhosin secure ext
RUN apt-get update &&  apt-get install -y php5-suhosin-extension

#Enviornment variables to configure php
ENV PHP_UPLOAD_MAX_FILESIZE 100M
ENV PHP_POST_MAX_SIZE 100M
