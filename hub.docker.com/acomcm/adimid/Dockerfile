FROM ubuntu:latest
MAINTAINER Ivan <ivan.petrus@acommerce.asia>

RUN echo PHP 7.0.10 && apt-get update && apt-get install -y software-properties-common

RUN LC_ALL=C.UTF-8 add-apt-repository ppa:ondrej/php

RUN apt-key adv --keyserver keyserver.ubuntu.com --recv-keys 4F4EA0AAE5267A6C

RUN echo PHP 7.0.10 && apt-get update && apt-get install -y \
	wget cron supervisor curl \
	php7.0-cli php7.0-common php7.0-curl php7.0-fpm php7.0-gd php7.0-mcrypt \
	php7.0-mysql php7.0-sqlite php7.0-readline php7.0-opcache \
	php7.0-mbstring php-ssh2 php7.0-bcmath php7.0-zip \
	php7.0-bz2 php7.0-json php7.0-dev build-essential \
	php-pear git pkg-config libssl-dev libsasl2-dev git && \
	apt-get clean

RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

