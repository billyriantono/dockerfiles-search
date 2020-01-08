##
# docker build -t floatapp/php7-yii2:dev-$(~/scripts/git-log-count.sh) .
# docker build -t floatapp/php7-yii2:$(~/scripts/git-log-count.sh) .

FROM php:7.2.24-apache-stretch

LABEL maintainer="tech@float.com"

# apt-get
RUN apt-get update && apt-get -y install \
    bzip2 git nano wget zip unzip \
    libmcrypt-dev libzzip-dev zziplib-bin zlib1g-dev \
    dialog apt-utils \
    && apt-get clean && rm -rf /var/lib/apt/lists/*

# docker-php ext-install: (include opcache)
## docker-php-ext-install mcrypt &&
RUN docker-php-ext-install zip && \
    docker-php-ext-install pdo_mysql && \
    docker-php-ext-install opcache

# phpredis
RUN pecl install redis-4.3.0 && docker-php-ext-enable redis
RUN pecl install mcrypt-1.0.1 && docker-php-ext-enable mcrypt

# optional net & proc tools:
# RUN apt-get -y install net-tools netcat telnet procps

# rsyslog: (optional: for Loggly etc)
# RUN apt-get update && apt-get -y install rsyslog && apt-get clean
# RUN sed -i '1s/^/$MaxMessageSize 64k\n/' /etc/rsyslog.conf

# apache mods:
RUN a2enmod rewrite
# if desired:
# && a2enmod headers

# AMQP
# ssl dep:
WORKDIR /opt
# openssl 1.0: http://ftp.se.debian.org/debian/pool/main/o/openssl/libssl1.0.0_1.0.2l-1~bpo8+1_amd64.deb
RUN wget http://ftp.se.debian.org/debian/pool/main/o/openssl/libssl1.1_1.1.0l-1~deb9u1_amd64.deb && \
    dpkg -i libssl1.1_1.1.0l-1~deb9u1_amd64.deb && \
    wget http://in.archive.ubuntu.com/ubuntu/ubuntu/pool/universe/libr/librabbitmq/librabbitmq4_0.8.0-1build1_amd64.deb && \
	wget http://in.archive.ubuntu.com/ubuntu/ubuntu/pool/universe/libr/librabbitmq/librabbitmq-dev_0.8.0-1build1_amd64.deb && \
    dpkg -i librabbitmq4_0.8.0-1build1_amd64.deb && dpkg -i librabbitmq-dev_0.8.0-1build1_amd64.deb && \
    pecl install amqp-1.9.4 && docker-php-ext-enable amqp

# composer:
COPY composer-install.sh /tmp
RUN /tmp/composer-install.sh && mv /usr/local/bin/composer.phar /usr/local/bin/composer && \
    /usr/local/bin/composer global require "fxp/composer-asset-plugin"

# copy pre-customized php ini files:
COPY docker/php/etc-php/conf-d /usr/local/etc/php/conf.d/
COPY docker/php/etc-php/php.ini /usr/local/etc/php/php.ini

COPY ./www/html /var/www/html
COPY ./www/composer.json /var/www/composer.json

RUN chown -R www-data /var/www
WORKDIR /var/www

USER www-data
RUN /usr/local/bin/composer install -o

USER root
