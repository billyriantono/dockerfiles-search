FROM php:5.6-apache
MAINTAINER Jakub Karkoszka <karkoszka@gmail.com>

COPY config/php.ini /usr/local/etc/php/
COPY src/ /var/www/html/

RUN apt-get update && apt-get install -y \
        vim \
        wget \
    	imagemagick \
    	p7zip-full \
    	syslinux \
    	syslinux-utils \
    	supervisor \
    	vim \
    	iputils-ping \
    	libxml2-dev \
    	host

RUN apt-get install -y \
        libfreetype6-dev \
        libjpeg62-turbo-dev \
        libmcrypt-dev \
        libpng12-dev \
    && docker-php-ext-install iconv mysql opcache pdo pdo_mysql zip mcrypt soap mbstring \
    && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
    && docker-php-ext-install gd

COPY ./configure.sh /
RUN ["chmod", "+x", "/configure.sh"]

ENTRYPOINT ["/configure.sh"]
