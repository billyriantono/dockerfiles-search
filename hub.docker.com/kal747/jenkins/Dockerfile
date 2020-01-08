FROM jenkins/jenkins:lts

MAINTAINER "Jeremy CURNY" <jeremy.curny.pro@gmail.com>

ARG DEBIAN_FRONTEND=noninteractive

RUN \
  curl -o /usr/local/bin/composer https://getcomposer.org/composer.phar \
  && chmod +x /usr/local/bin/composer

RUN apt-get update && apt-get install -y \
  php-cli \
  php-curl php-gd php-imap php-intl php-mbstring php-mcrypt php-memcache php-mysql php-sqlite3 php-xsl \
  \
  jpegoptim optipng
