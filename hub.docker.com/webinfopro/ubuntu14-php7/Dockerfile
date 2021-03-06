#!/usr/bin/env docker

FROM ubuntu:14.04
MAINTAINER Frédéric HENNINOT

ENV INITRD=No TERM=dumb MY_TZ=Europe/Paris
ENV DEBIAN_FRONTEND noninteractive

RUN rm /etc/timezone && echo $MY_TZ >> /etc/timezone && locale-gen fr_FR.UTF-8 && LC_ALL=fr_FR.UTF-8

# Install LAMP stack
RUN apt-get update
RUN apt-get install -y python-software-properties software-properties-common
RUN LC_ALL=fr_FR.UTF-8 add-apt-repository ppa:ondrej/apache2 -y && LC_ALL=fr_FR.UTF-8 add-apt-repository ppa:ondrej/php -y && apt-get update

RUN apt-get install -y --force-yes \
	build-essential \
	imagemagick \
	ca-certificates \
	apache2 \
	libapache2-mod-php7.0 \
	php7.0 \
	php7.0-cli \
	php7.0-dev \
	php7.0-bcmath \
	php7.0-bz2 \
	php7.0-mysql \
	php7.0-mbstring \
	php7.0-mcrypt \
	php7.0-gd \
	php-imagick \
	php7.0-curl \
	php7.0-intl \
	php7.0-common \
	php7.0-json \
	php7.0-opcache \
	php7.0-recode \
	php7.0-soap \
	php7.0-xml \
	php7.0-zip \
	php7.0-opcache \
	php-apcu \
	php-gettext \
	phpmyadmin \
	default-jre \
	mysql-server \
	git \
	rsyslog \
	curl  \
	wget \
	nano

# Enable Apache module
RUN a2enmod rewrite ssl && a2dismod php5
RUN ln -s  /etc/phpmyadmin/apache.conf /etc/apache2/conf-enabled/phpmyadmin.conf

# Install Composer
RUN curl https://getcomposer.org/installer | php -- && mv composer.phar /usr/local/bin/composer && chmod +x /usr/local/bin/composer

RUN apt-get autoclean && apt-get autoremove && apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*
