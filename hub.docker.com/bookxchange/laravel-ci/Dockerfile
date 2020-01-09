FROM php:7.1-cli

# Update packages and install composer and PHP dependencies.
RUN apt-get update -yqq && apt-get install -yqq \
	git \
	libcurl4-gnutls-dev \
	libicu-dev \
	libvpx-dev \
	libjpeg-dev \
	libpng-dev \
	libxpm-dev \
	zlib1g-dev \
	libfreetype6-dev \
	libxml2-dev \
	libexpat1-dev \
	libbz2-dev \
	libgmp3-dev \
	libldap2-dev \
	unixodbc-dev \
	libpq-dev \
	libsqlite3-dev \
	libaspell-dev \
	libsnmp-dev \
	libpcre3-dev \
	libtidy-dev

# Compile PHP, include these extensions.
RUN docker-php-ext-install \
	mbstring \
	pdo_mysql \
	pdo_pgsql \
	curl \
	json \
	intl \
	gd \
	xml \
	zip \
	bz2 \
	opcache

# Install Composer.
RUN curl -sS https://getcomposer.org/installer | php
RUN chmod 755 composer.phar && mv composer.phar /usr/local/bin/composer
