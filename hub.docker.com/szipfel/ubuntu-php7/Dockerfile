FROM ubuntu:16.04
MAINTAINER Steve Zipfel <steve@webrepublic.ca>
RUN rm /bin/sh && ln -s /bin/bash /bin/sh

# Install packages.
RUN apt-get update
RUN apt-get purge `dpkg -l | grep php| awk '{print $2}' |tr "\n" " "`
RUN apt-get install -y software-properties-common python-software-properties
RUN LC_ALL=C.UTF-8 add-apt-repository ppa:ondrej/php
RUN apt-get update
RUN apt-get install -y vim git apache2 php5.6 curl wget \
php5.6-gd php5.6-dom php5.6-curl php5.6-mbstring php5.6-bz2 php5.6-bcmath php5.6-soap php5.6-simplexml \
php5.6-xml php5.6-cli php5.6-mysql \
supervisor unzip composer php-mysql mysql-client

RUN apt-get clean
RUN a2enmod rewrite
#Start up Apache
RUN /etc/init.d/apache2 start

EXPOSE 80 
CMD exec supervisord -n
