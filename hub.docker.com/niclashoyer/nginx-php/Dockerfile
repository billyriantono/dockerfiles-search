FROM ubuntu:precise

MAINTAINER Niclas Hoyer "niclas.hoyer@splendid-internet.de"

ENV DEBIAN_FRONTEND noninteractive

RUN echo "deb http://archive.ubuntu.com/ubuntu/ precise universe" >> /etc/apt/sources.list
RUN apt-get update
RUN apt-get -y install dialog net-tools vim wget curl python-software-properties supervisor
RUN add-apt-repository -y ppa:nginx/stable
RUN add-apt-repository -y ppa:ondrej/php5 > /dev/null 2>&1 # dirty fix for "invalid UTF-8 in string"
RUN apt-get update
RUN apt-get -y install ssl-cert nginx php5-fpm php5-mysql php-apc php5-imagick php5-gd php5-imap php5-mcrypt php5-curl php5-mcrypt php5-redis php5-dev php5-cli php-pear
RUN pecl install mongo
RUN echo "extension=mongo.so" > /etc/php5/fpm/conf.d/mongo.ini
RUN echo "cgi.fix_pathinfo=0;" >> /etc/php5/fpm/php.ini
RUN echo "daemon off;" >> /etc/nginx/nginx.conf
RUN mkdir -p /var/www
RUN echo "<?php phpinfo(); ?>" > /var/www/phpinfo.php

ADD supervisor/nginx.conf   /etc/supervisor/conf.d/nginx.conf
ADD supervisor/php.conf     /etc/supervisor/conf.d/php.conf

ADD nginx/include.d         /etc/nginx/include.d
ADD nginx/default           /etc/nginx/sites-available/default
ADD nginx/index.html        /var/www/index.html

EXPOSE 443
EXPOSE 80

VOLUME [ "/var/www" ]

CMD [ "/usr/bin/supervisord", "-n" ]

