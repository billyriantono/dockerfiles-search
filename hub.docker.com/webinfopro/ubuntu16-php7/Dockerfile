#!/usr/bin/env docker

FROM ubuntu:16.04
MAINTAINER Frédéric HENNINOT

ENV INITRD=No TERM=dumb MY_TZ=Europe/Paris
ENV DEBIAN_FRONTEND noninteractive

# Install LAMP stack
RUN apt-get update
RUN apt-get install -y locales python-software-properties software-properties-common && apt-get update && apt-get -qq upgrade

RUN rm /etc/timezone && echo $MY_TZ >> /etc/timezone && locale-gen fr_FR.UTF-8 && LC_ALL=fr_FR.UTF-8

RUN LC_ALL=fr_FR.UTF-8 add-apt-repository ppa:ondrej/mysql-5.6 -y && apt-get update

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
	mysql-server-5.6 \
	git \
	rsyslog \
	curl  \
	wget \
	nano

# Enable Apache module
RUN a2enmod rewrite ssl
RUN ln -s  /etc/phpmyadmin/apache.conf /etc/apache2/conf-enabled/phpmyadmin.conf

# Install Composer
RUN curl https://getcomposer.org/installer | php -- && mv composer.phar /usr/local/bin/composer && chmod +x /usr/local/bin/composer

# Install Insight.phar 
RUN curl -o insight.phar -s http://get.insight.sensiolabs.com/insight.phar && mv insight.phar /usr/local/bin/ && chmod +x /usr/local/bin/insight.phar

# Install Deployer
RUN curl -LO https://deployer.org/deployer.phar && mv deployer.phar /usr/local/bin/dep && chmod +x /usr/local/bin/dep

# Install PHPUnit.phar
RUN wget https://phar.phpunit.de/phpunit.phar && chmod +x phpunit.phar && mv phpunit.phar /usr/local/bin/phpunit

# Install PHPMetrics
RUN wget https://github.com/phpmetrics/PhpMetrics/raw/master/build/phpmetrics.phar && chmod +x phpmetrics.phar && mv phpmetrics.phar /usr/local/bin/phpmetrics

# Install some testing script
RUN composer global require phpdocumentor/phpdocumentor && composer global require sebastian/phpcpd 2.0 && composer global require phploc/phploc && composer global require phpmd/phpmd && composer global require escapestudios/symfony2-coding-standard

RUN apt-get autoclean && apt-get autoremove && apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*
