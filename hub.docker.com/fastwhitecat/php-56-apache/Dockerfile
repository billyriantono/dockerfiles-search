FROM php:5.6.20-apache

RUN apt-get update \
  && apt-get install -y \
	git-core \
	bzip2\
	zip\
    zlib1g-dev\
    libmcrypt-dev\
	libicu-dev\
	libcurl4-openssl-dev\
	libfreetype6-dev\
	libgd-dev\
	libxml2-dev\
	libexif-dev \
	libjpeg-dev \
	g++\
	unzip\
	mysql-client\
	openssl \
	cron \
	sudo \
	vim \
	supervisor\
  && apt-get clean

RUN docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
&& docker-php-ext-install -j$(nproc) gd

RUN docker-php-ext-install \
    mcrypt \
    intl \
    pdo_mysql \
    curl \
    soap \
    xml \
    exif \
    zip

RUN curl -sS https://getcomposer.org/installer | \
    php -- \
      --install-dir=/usr/local/bin \
      --filename=composer \
      --version=1.1.2

RUN pecl install apcu-4.0.11 \
     && docker-php-ext-enable apcu

RUN a2enmod rewrite
RUN a2enmod ssl
