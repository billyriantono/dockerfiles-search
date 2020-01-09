FROM php:5.6.8-apache

RUN apt-get update && apt-get install -y vim git php5-cli php5-curl php5-mysql wget phpunit mysql-client php5-xdebug libxml2-dev && apt-get clean

RUN curl -sS https://getcomposer.org/installer | php
RUN mv composer.phar /usr/sbin/composer

RUN wget http://get.sensiolabs.org/php-cs-fixer.phar -O php-cs-fixer && chmod a+x php-cs-fixer && mv php-cs-fixer /usr/local/bin/php-cs-fixer

RUN a2enmod rewrite
RUN a2enmod headers

ADD .gitconfig /root/.gitconfig
ADD .bashrc /root/.bashrc
