FROM ubuntu:19.04
MAINTAINER Balint Dozsa <balint.do89@gmail.com>

# nginx
RUN apt-get update && \
	DEBIAN_FRONTEND=noninteractive apt-get install -y \
	software-properties-common \
	supervisor \
	curl \
	nginx

# php
RUN LC_ALL=C.UTF-8 add-apt-repository -y ppa:ondrej/php && \
	DEBIAN_FRONTEND=noninteractive apt-get install -y \
	php7.3 \
	php7.3-fpm \
	php7.3-curl \
	php7.3-json \
	php7.3-mbstring \
	php7.3-mysql \
	php7.3-opcache \
	php7.3-readline \
	php7.3-xml \
	php7.3-zip \
	php-xdebug \
	mysql-client

# composer
RUN curl -o /usr/local/bin/composer https://getcomposer.org/composer.phar && \
	chmod +x /usr/local/bin/composer

# backup
RUN mkdir /bckp
RUN cp /etc/nginx/nginx.conf /bckp/ && \
	cp /etc/nginx/sites-enabled/default /bckp/ && \
	cp /etc/php/7.3/cli/php.ini /bckp/cli_php.ini && \
	cp /etc/php/7.3/fpm/php-fpm.conf /bckp/ && \
	cp /etc/php/7.3/fpm/php.ini /bckp/fpm_php.ini

# copy conf files
COPY files/ /

# project dir
RUN mkdir /project
WORKDIR /project

# php fpm
RUN mkdir -p /run/php

# 80
EXPOSE 80

CMD ["/usr/bin/supervisord"]
