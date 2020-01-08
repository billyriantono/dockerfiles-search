# from https://www.drupal.org/requirements/php#drupalversions
FROM php:7.2.2-fpm-alpine3.7

RUN apk update
RUN apk add vim \
	git \
	nginx \
	php7-mysqli \
	php7-gd \
	php7-curl \
	php7-xdebug \
	php7-sqlite3 \
	curl \
	mysql \
	mysql-client \
	openssh \ 
	wget \
	unzip \
	gnupg \
	supervisor

RUN mkdir /run/nginx

# Setup PHP
#RUN sed -i 's/display_errors = Off/display_errors = On/' /etc/php7/php.ini

#================================================
# Install openssh
# https://docs.docker.com/engine/examples/running_ssh_service/
# TODO: replace chpasswd with: mkpasswd -m md5 '...' + usermod -p'$1...' root
#RUN apk update && apk add openssh && \
#    mkdir /var/run/sshd && \
#    echo 'root:root' | chpasswd && \
#    sed -i 's/PermitRootLogin prohibit-password/PermitRootLogin yes/' /etc/ssh/sshd_config

#RUN adduser -D -u 1000 quentin


#WORKDIR /var/www

#VOLUME /home/quentin/DEV/drupal/
