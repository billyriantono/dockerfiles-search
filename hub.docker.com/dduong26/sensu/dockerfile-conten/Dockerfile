FROM debian:jessie-slim

MAINTAINER James Meers <james@daveslab.co.uk>

ADD . /app
WORKDIR /app

## Set the terminal to be Noninteractive
ENV DEBIAN_FRONTEND noninteractive

## Clean, update...
RUN apt-get update -y && \
    apt-get install -y --no-install-recommends apt-utils

## ... & upgrade
RUN apt-get update -y && \
    apt-get upgrade -y

## Install essential software
RUN apt-get update
RUN apt-get install -y software-properties-common \
                       python \
                       zip \
                       unzip \
                       git-all \
                       nano \
                       vim \
                       wget \
                       curl \
                       jq

## Download and install pip (for AWS-CLI install)
RUN curl -O https://bootstrap.pypa.io/get-pip.py
RUN python3 get-pip.py

## Install AWS CLI
RUN pip install awscli --upgrade

## Install other stuff... MEMCACHED!
RUN apt-get update
RUN apt-get install -y mlocate \
                       telnet \
                       links \
                       lynx \
                       heirloom-mailx \
                       iotop \
                       htop \
                       rsyslog-gnutls \
                       libmemcached-dev \
                       memcached

## Install apache2 & mod_ssl packages
RUN apt-get update
RUN apt-get install -y apache2 \
                       ssl-cert \
                       libapache2-modsecurity

## Enable apache2 modules
RUN a2enmod headers \
            proxy \
            proxy_balancer \
            proxy_http \
            rewrite \
            socache_shmcb \
            ssl \
            security2

## Copy Apache config
COPY apache/apache2.conf /etc/apache2/apache2.conf
COPY apache/vhost.conf /etc/apache2/sites-available/000-default.conf

## Install PHP 7
RUN apt-add-repository 'deb http://packages.dotdeb.org jessie all' && \
    cd ~ && \
    wget https://www.dotdeb.org/dotdeb.gpg && \
    apt-key add dotdeb.gpg

RUN apt-get update
RUN apt-get install -y php7.0 \
                       libapache2-mod-php7.0 \
                       php7.0-intl \
                       php7.0-gd \
                       php7.0-mysql \
                       php7.0-xml \
                       php7.0-mbstring \
                       php7.0-apcu \
                       php7.0-apcu-bc \
                       php7.0-memcached \
                       php7.0-bcmath \
                       php7.0-mcrypt \
                       php7.0-cli \
                       php7.0-curl

## Install PHPUnit
RUN wget https://phar.phpunit.de/phpunit-6.1.phar
RUN chmod +x phpunit-6.1.phar
RUN mv phpunit-6.1.phar /usr/local/bin/phpunit
RUN phpunit --version

## Install Composer
RUN curl --silent --show-error https://getcomposer.org/installer | php
RUN mv composer.phar /usr/local/bin/composer
RUN chmod +x /usr/local/bin/composer

## Install NodeJS
RUN curl -sL https://deb.nodesource.com/setup_6.x -o nodesource_setup.sh
RUN bash nodesource_setup.sh
RUN apt-get install -y nodejs

## Install essential NodeJS packages for asset management in Symfony
RUN npm install bower -g
RUN npm install less -g
RUN npm install uglifycss -g
RUN npm install uglify-js -g

RUN usermod -u 1000 www-data

## Setup some aliases
RUN touch /root/.bashrc \
    echo "alias dir='ls -alh'" >> /root/.bashrc \
    echo "alias pico='nano -c'" >> /root/.bashrc \
    source /root/.bashrc