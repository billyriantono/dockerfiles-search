FROM php:5.6
MAINTAINER Anton Kochnev <antcheri@gmail.com>

RUN apt-get update
RUN apt-get install -y git
#Composer
RUN curl -sS https://getcomposer.org/installer | php
RUN mv composer.phar /usr/local/bin/composer