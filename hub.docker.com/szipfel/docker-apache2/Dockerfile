FROM ubuntu:16.04
MAINTAINER Steve Zipfel <steve@webrepublic.ca>
RUN rm /bin/sh && ln -s /bin/bash /bin/sh

# Install packages.
RUN apt-get update
RUN apt-get install -y software-properties-common python-software-properties
RUN LC_ALL=C.UTF-8 add-apt-repository ppa:ondrej/php
RUN apt-get update
RUN apt-get install -y vim git apache2 php7.1 curl wget \
php7.1-gd php7.1-common php7.1-dom php7.1-xml php7.1-curl php7.1-mbstring php7.1-bz2 php7.1-bcmath \
libapache2-mod-php7.1 supervisor unzip composer php7.1-mysql mysql-client \ 
libc6 libxml2 ucf php7.1-fpm php7.1-cli php7.1-common php7.1-xmlrpc php7.1-soap php7.1-memcached

RUN apt-get clean
RUN a2enmod rewrite
#Start up Apache
RUN /etc/init.d/apache2 start

EXPOSE 80 
CMD exec supervisord -n
