# ubuntu-apache
#
# VERSION               0.0.1

FROM      gendosu/ubuntu-base:latest

MAINTAINER Gen Takahashi <gendosu@gmail.com>

ENV APACHE_RUN_USER="www-data"
ENV APACHE_RUN_GROUP="www-data"
ENV APACHE_LOG_DIR="log"

RUN apt-get update \
&&  apt-get upgrade -y --force-yes \
&&  apt-get install -y --force-yes \
    libssl-dev \
    libreadline-dev \
    imagemagick \
    libmagick++-dev \
    libqtwebkit-dev \
    xvfb \
    libffi-dev \
    mysql-client \
    libmysqlclient-dev \
    libssl-dev \
    zip \
    vim \
    build-essential \
    apache2 \
    php \
    php-mysql \
&&  apt-get clean \
&&  rm -rf /var/cache/apt/archives/* /var/lib/apt/lists/*

RUN mkdir -p /etc/apache/log

RUN a2enmod rewrite

CMD /usr/sbin/apache2 -DFOREGROUND

