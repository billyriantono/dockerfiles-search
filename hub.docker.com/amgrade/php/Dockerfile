FROM ubuntu:14.04
MAINTAINER Artem Berdyshev "a.berdyshev@amgrade.com"

ENV DEBIAN_FRONTEND noninteractive

# Set timezone and locale.
RUN locale-gen en_US.UTF-8
ENV LANG en_US.UTF-8
ENV LANGUAGE en_US:en
ENV LC_ALL en_US.UTF-8

RUN apt-get -y update && \
    apt-get -y install \
    php5-mysql \
    php5-mcrypt \
    php5-intl \
    php5-memcached \
    php5-json \
    php5-gd \
    imagemagick php5-imagick \
    php5-curl \
    php-pear \
    php-apc \
    php5-apcu \
    php5-xdebug \
    php5-xmlrpc \
    php5-xsl \
    php5-sqlite \
    sqlite3 && \
    rm -rf /var/lib/apt/lists/* && \
    apt-get clean

COPY xdebug.ini /etc/php5/mods-available/xdebug.ini

CMD ["/usr/bin/php", "--help"]
