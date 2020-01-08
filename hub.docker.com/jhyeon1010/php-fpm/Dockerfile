FROM ubuntu:14.04

MAINTAINER jhyeon1010 "jhyeon1010@naver.com"

ENV DEBIAN_FRONTEND noninteractive

RUN apt-get update
RUN apt-get install -y software-properties-common language-pack-en-base zip unzip

# install php
RUN LC_ALL=en_US.UTF-8 add-apt-repository -y ppa:ondrej/php
RUN apt-get update
RUN apt-get install -y \
    php7.0 \
    php7.0-fpm \
    php7.0-curl \
    php7.0-gd \
    php7.0-gmp \
    php7.0-imap \
    php7.0-mcrypt \
    php7.0-tidy \
    php7.0-xmlrpc \
    php7.0-xsl \
    php7.0-mysql \
    php7.0-bcmath \
    php7.0-mbstring \
    php7.0-soap \
    php7.0-xml \
    php7.0-zip \
    php-memcached \
    && mkdir /var/run/php

ARG UID=1000
RUN usermod -u $UID www-data

VOLUME /var/www/html
VOLUME /var/run/php

CMD ["php-fpm7.0", "-F"]

EXPOSE 9000

