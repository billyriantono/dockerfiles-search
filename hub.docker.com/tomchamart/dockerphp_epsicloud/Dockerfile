FROM debian:wheezy
RUN apt-get update -qq && apt-get upgrade -y
RUN apt-get install wget -qq

RUN apt-get update \
  && apt-get install -y --force-yes \
  php5 \
  php5-fpm \
  php5-cli \
  php5-mysql \
  php5-mcrypt \
  php5-curl \
  php5-gd \
  php5-intl

RUN apt-get clean \
  && rm -rf /var/lib/apt/lists/* \
  /tmp/* \
  /var/tmp/*

RUN php5enmod mcrypt
