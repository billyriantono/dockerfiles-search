FROM php:7.1.24-fpm

MAINTAINER Mitch Daniels <m.daniels@serv-ict.nl>

# Set debconf to run non-interactively
RUN echo 'debconf debconf/frontend select Noninteractive' | debconf-set-selections

# replace shell with bash so we can source files
RUN rm /bin/sh && ln -s /bin/bash /bin/sh

COPY resources/bin/* /usr/local/bin/
RUN chmod -R 775 /usr/local/bin/

RUN echo "Europe/Amsterdam" > /etc/timezone && dpkg-reconfigure -f noninteractive tzdata

RUN apt-get update \
  && apt-get install -y \
    git \
    cron \
    libfreetype6-dev \
    libicu-dev \
    libjpeg62-turbo-dev \
    libmcrypt-dev \
	libpng-dev \
    libxslt1-dev \
    python-pip \
    redis-tools \
    supervisor \
	python \
	openssl \
	curl  \
	gcc \
	g++ \
	unzip \
	jq \
	git-core \
	libssl-dev \
	zip \
	build-essential \
	vim

# AWS cli is nice to have on aws, think: PaaS.
RUN pip install awsebcli --upgrade --user

# PHP
# intl
RUN apt-get update \
	&& apt-get install -y libicu-dev \
	&& docker-php-ext-configure intl \
	&& docker-php-ext-install -j$(nproc) intl

# xml
RUN apt-get update \
	&& apt-get install -y \
	libxml2-dev \
	libxslt-dev \
	&& docker-php-ext-install -j$(nproc) \
		dom \
		xmlrpc \
		xsl

# images
RUN apt-get update \
	&& apt-get install -y \
	libfreetype6-dev \
	libjpeg62-turbo-dev \
	libpng-dev \
	libgd-dev \
	&& docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
	&& docker-php-ext-install -j$(nproc) \
		gd \
		exif

# database
RUN docker-php-ext-install -j$(nproc) \
	mysqli \
	pdo \
	pdo_mysql

# strings
RUN docker-php-ext-install -j$(nproc) \
	gettext \
	mbstring

# math
RUN apt-get update \
	&& apt-get install -y libgmp-dev \
	&& ln -s /usr/include/x86_64-linux-gnu/gmp.h /usr/include/gmp.h \
	&& docker-php-ext-install -j$(nproc) \
		gmp \
		bcmath

# compression
RUN apt-get update \
	&& apt-get install -y \
	libbz2-dev \
	zlib1g-dev \
	&& docker-php-ext-install -j$(nproc) \
		zip \
		bz2

# ftp
RUN apt-get update \
	&& apt-get install -y \
	libssl-dev \
	&& docker-php-ext-install -j$(nproc) \
		ftp

# ssh2
RUN apt-get update \
	&& apt-get install -y \
	libssh2-1-dev

# memcached
RUN apt-get update \
	&& apt-get install -y \
	libmemcached-dev \
	libmemcached11

# others
RUN docker-php-ext-install -j$(nproc) \
	soap \
	sockets \
	calendar \
	sysvmsg \
	sysvsem \
	sysvshm

# PECL
RUN docker-php-pecl-install \
	ssh2-1.1.2 \
	redis-4.0.2 \
	apcu-5.1.11 \
	memcached-3.0.4

# Install composer and put binary into $PATH
RUN curl -sS https://getcomposer.org/installer | php \
	&& mv composer.phar /usr/local/bin/ \
	&& ln -s /usr/local/bin/composer.phar /usr/local/bin/composer

# nvm environment variables
ENV NVM_DIR /usr/local/nvm
ENV NODE_VERSION 4.4.7

# install nvm
# https://github.com/creationix/nvm#install-script
RUN curl --silent -o- https://raw.githubusercontent.com/creationix/nvm/v0.31.2/install.sh | bash

# install node and npm
RUN source $NVM_DIR/nvm.sh \
    && nvm install $NODE_VERSION \
    && nvm alias default $NODE_VERSION \
    && nvm use default

# add node and npm to path so the commands are available
ENV NODE_PATH $NVM_DIR/v$NODE_VERSION/lib/node_modules
ENV PATH $NVM_DIR/versions/node/v$NODE_VERSION/bin:$PATH

# confirm installation
RUN node -v
RUN npm -v

# update and install last apps
RUN apt-get update && apt-get install -y gcc g++ unzip jq

# Clean
RUN apt-get clean

# Copy custom configs
COPY resources/conf/php.ini /usr/local/etc/php/
COPY resources/conf/php-fpm.conf /usr/local/etc/
COPY resources/conf/laravel-worker.conf /etc/supervisor/conf.d/

# Go to dir
WORKDIR /var/www/html

# Create env file and folder
RUN mkdir -p /tmp/envs && touch /tmp/envs/env_file

# Env details
ENV APP_DIR "/var/www/html"
ENV PHP_MEMORY_LIMIT 512M
ENV PHP_POST_MAX_SIZE 64M
ENV PHP_UPLOAD_MAX_SIZE: 64M
ENV PHP_MAX_EXECUTION_TIME: 120
ENV PHP_SHORT_TAG: on
ENV PHP_PORT 9000
ENV PHP_PM dynamic
ENV PHP_PM_MAX_CHILDREN 10
ENV PHP_PM_START_SERVERS 4
ENV PHP_PM_MIN_SPARE_SERVERS 2
ENV PHP_PM_MAX_SPARE_SERVERS 6
ENV LARAVEL_QUEUE_WORKER_CONNECTION "sqs"
ENV LARAVEL_QUEUE_WORKER_SLEEP 3
ENV LARAVEL_QUEUE_WORKER_TRIES 3
ENV LARAVEL_QUEUE_WORKER_NUMPROCS 4
ENV LARAVEL_QUEUE_WORKER_TIMEOUT 60

# Start app and load variables in
CMD eval `cat /tmp/envs/env_file`; /usr/local/bin/start-laravel;