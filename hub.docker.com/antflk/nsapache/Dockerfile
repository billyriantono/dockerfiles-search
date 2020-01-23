FROM ubuntu:14.04
RUN apt-get update && apt-get upgrade -y

RUN locale-gen ru_RU.UTF-8 && locale-gen en_US.UTF-8 && dpkg-reconfigure locales

#time
RUN mv /etc/localtime /etc/localtime-old && ln -s /usr/share/zoneinfo/Europe/Moscow /etc/localtime

RUN apt-get install -y gcc make g++ build-essential libc6-dev tcl wget php5 php-pear php5-dev git tzdata apache2 curl php5-curl libcurl3 libcurl4-openssl-dev \
php5-mysql php5-gd gnumeric php5-imagick php5-cli  php5-imap php5-intl php5-xmlrpc  php5-xdebug php-http libpcre3-dev libevent-dev libmagic-dev make php5-mcrypt \
php5-memcached librabbitmq1 librabbitmq-dev make graphviz zip nodejs libssh2-php

#Установка апача
RUN a2enmod rewrite && a2enmod headers

#Установка pecl модулей
RUN yes | pecl install redis amqp  apcu-4.0.7 xhprof-0.9.4 raphf propro  pecl_http-1.7.6