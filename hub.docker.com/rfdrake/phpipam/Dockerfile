FROM php:5.6-apache
MAINTAINER Pierre Cheynier <pierre.cheynier@sfr.com>

ENV PHPIPAM_SOURCE https://github.com/phpipam/phpipam.git
ENV PHPIPAM_VERSION 1.2
ENV DB_HOST mysql
ENV DB_USER root

# Install required deb packages
RUN apt-get update && \ 
	apt-get install -y git php-pear php5-curl php5-mysql php5-json php5-gmp php5-mcrypt php5-ldap libgmp-dev libmcrypt-dev \
                       libldap2-dev && \
	rm -rf /var/lib/apt/lists/*

# Configure apache and required PHP modules 
RUN docker-php-ext-configure mysqli --with-mysqli=mysqlnd && \
	docker-php-ext-install mysqli && \
	docker-php-ext-install pdo_mysql && \
	docker-php-ext-install gettext && \ 
	ln -s /usr/include/x86_64-linux-gnu/gmp.h /usr/include/gmp.h && \
	docker-php-ext-configure gmp --with-gmp=/usr/include/x86_64-linux-gnu && \
	docker-php-ext-install gmp && \
    docker-php-ext-install mcrypt && \
    docker-php-ext-configure ldap --with-libdir=lib/x86_64-linux-gnu/ && \
    docker-php-ext-install ldap && \
	echo ". /etc/environment" >> /etc/apache2/envvars && \
	a2enmod rewrite

COPY php.ini /usr/local/etc/php/

# copy phpipam sources to web dir
RUN git clone --depth 1 -b ${PHPIPAM_VERSION} ${PHPIPAM_SOURCE} /tmp/phpipam && \
    cp -ar /tmp/phpipam/* /tmp/phpipam/.htaccess /var/www/html

# Use system environment variables into config.php
RUN sed \ 
	-e "s/db\['host'\] = \"localhost\"/db\['host'\] = getenv(\"DB_HOST\")/" \ 
    -e "s/db\['user'\] = \"phpipam\"/db\['user'\] = getenv(\"DB_USER\")/" \ 
    -e "s/db\['pass'\] = \"phpipamadmin\"/db\['pass'\] = getenv(\"DB_PASS\")/" \ 
	/var/www/html/config.dist.php > /var/www/html/config.php

EXPOSE 80

