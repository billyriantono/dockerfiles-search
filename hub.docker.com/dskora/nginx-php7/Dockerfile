FROM ubuntu:14.04

# install packages for Apache and for compiling PHP
RUN apt-get update && apt-get install -y \
    python-setuptools \
    nginx \
    libcurl4-openssl-dev \
    libmcrypt-dev \
    libxml2-dev \
    libjpeg-dev \
    libfreetype6-dev \
    libmysqlclient-dev \
    libt1-dev \
    libgmp-dev \
    libpspell-dev \
    libicu-dev \
    librecode-dev \
    libjpeg62 \
    git \
    wget

# PHP 7 beta
ADD http://repos.zend.com/zend-server/early-access/php7/php-7.0-beta1-DEB-x86_64.tar.gz /usr/local/php7

RUN tar zxPf /usr/local/php7
ENV PATH $PATH:/usr/local/php7/bin

ENV PATH=$PATH:/usr/local/php7/bin

COPY conf/nginx/vhost.conf /etc/nginx/sites-available/default
COPY conf/supervisord/supervisord.conf /etc/supervisord.conf
COPY conf/fpm-init.php /opt/fpm-init.php

COPY conf/etc/ /usr/local/php7/etc

EXPOSE 80

# Supervisor Install
RUN /usr/bin/easy_install supervisor

# Run supervisor
CMD ["/usr/local/bin/supervisord", "-n"]
