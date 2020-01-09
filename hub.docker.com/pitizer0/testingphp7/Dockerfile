# Version 1
FROM debian:7
MAINTAINER Jose M. Rios "josefeelmotion@gmail.com"
RUN echo "deb http://deb.debian.org/debian wheezy-backports main" >> /etc/apt/sources.list
RUN apt-get update 
RUN apt-get install -y apache2 php5 php5-xdebug php5-imagick php5-xmlrpc git php5-cli nodejs mysql-server-5.5=5.5.47-0+deb7u1 wget
RUN wget https://raw.githubusercontent.com/composer/getcomposer.org/1b137f8bf6db3e79a38a5bc45324414a6b1f9df2/web/installer -O - -q | php -- --quiet
EXPOSE 80
