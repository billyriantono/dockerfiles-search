FROM ubuntu:15.04
MAINTAINER Henrik Schmidt <henrik@henrik-schmidt.de>

ENV DEBIAN_FRONTEND noninteractive

WORKDIR /root
USER root

RUN apt-get update
RUN apt-get upgrade -y
RUN apt-get install -y software-properties-common

RUN apt-add-repository -y ppa:phalcon/stable
RUN apt-get update

RUN apt-get install -y curl git php5 php5-cli php5-phalcon php5-xdebug

RUN curl -sS https://getcomposer.org/installer | php
RUN mv composer.phar /usr/local/bin/composer
