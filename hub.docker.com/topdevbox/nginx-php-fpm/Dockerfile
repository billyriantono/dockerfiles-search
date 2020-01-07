FROM topdevbox/base
MAINTAINER Daniel <daniel@topdevbox.com>
# How-To
# Local Build: docker build -t my/web:test .
# Local Run: docker run -i -t --name="web" -v ~/temp/data:/var/data my/web:test /bin/bash
# Deamon Run: docker run -d --name web -p 80:80 -p 443:443 -v ~/temp/data:/var/data my/web:test

RUN apt-get update && \
	apt-get upgrade -y && \
	apt-get autoclean && \
	apt-get autoremove && \
    apt-get clean

RUN apt-get install -y nano \
			curl \
			nginx \
			mysql-client \
			openssl \
			php \
			php-fpm \
			php-xml \
			php-mbstring \
			php-bcmath \
			php-zip \
			php-mysql \
			php-pdo-mysql \
			php-curl  \
			php-gd \
			php-intl \
			php-pear \
			php-imagick \
			php-imap \
			php-mcrypt \
			php-memcache \
			php-apcu \
			php-pspell \
			php-recode \
			php-tidy \
			php-xmlrpc \
			php-json \
			php-bz2 \
			php-opcache && \
	mkdir /var/data && \
	chown -R www-data:www-data /var/data

# 	VALUME POINTS
#	 - /etc/php
#	 - /etc/nginx

RUN curl -O https://bin.equinox.io/c/ekMN3bCZFUn/forego-stable-linux-amd64.tgz \
 && tar -xzf forego-stable-linux-amd64.tgz -C /usr/bin \
 && rm forego-stable-linux-amd64.tgz \
 && mkdir -p /run/php \
 && mkdir -p /etc/letsencrypt


VOLUME /var/data
VOLUME /etc/php
VOLUME /etc/nginx
VOLUME /etc/letsencrypt

#CMD COPY CONFIG FILE TO /var/data
RUN mkdir -p /var/temp && \
	cp -R /etc/nginx /var/temp/nginx && \
	cp -R /etc/php /var/temp/php

ADD Procfile /Procfile
ADD Procfile /usr/bin/Procfile

EXPOSE 443 80

ENTRYPOINT forego start
