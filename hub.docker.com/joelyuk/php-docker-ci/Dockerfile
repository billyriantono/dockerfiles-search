FROM php:7.0-fpm

MAINTAINER Jaroslav Hranicka <hranicka@outlook.com>

ENV DEBIAN_FRONTEND noninteractive
COPY bin/* /usr/local/bin/
RUN chmod -R 700 /usr/local/bin/


# Locales
	RUN apt-get update \
		&& apt-get install -y locales

	RUN dpkg-reconfigure locales \
		&& locale-gen C.UTF-8 \
		&& /usr/sbin/update-locale LANG=C.UTF-8

	RUN echo 'en_US.UTF-8 UTF-8' >> /etc/locale.gen \
		&& locale-gen

	ENV LC_ALL C.UTF-8
	ENV LANG en_US.UTF-8
	ENV LANGUAGE en_US.UTF-8


# Common
	RUN apt-get update \
		&& apt-get install -y \
			openssl \
			git \
			make \
			curl

# PHP
	# intl
	RUN apt-get update \
		&& apt-get install -y libicu-dev \
		&& docker-php-ext-configure intl \
		&& docker-php-ext-install intl

	# xml
	RUN apt-get update \
		&& apt-get install -y \
		libxml2-dev \
		libxslt-dev \
		&& docker-php-ext-install \
			dom \
			xmlrpc \
			xsl

	# images
	RUN apt-get update \
		&& apt-get install -y \
		libfreetype6-dev \
		libjpeg62-turbo-dev \
		libpng12-dev \
		libgd-dev \
		&& docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
		&& docker-php-ext-install \
			gd \
			exif

	# database
	RUN docker-php-ext-install \
		mysqli \
		pdo \
		pdo_mysql

	# mcrypt
	RUN apt-get update \
		&& apt-get install -y libmcrypt-dev \
		&& docker-php-ext-install mcrypt

	# strings
	RUN docker-php-ext-install \
		gettext \
		mbstring

	# math
	RUN apt-get update \
		&& apt-get install -y libgmp-dev \
		&& ln -s /usr/include/x86_64-linux-gnu/gmp.h /usr/include/gmp.h \
		&& docker-php-ext-install \
			gmp \
			bcmath

	# compression
	RUN apt-get update \
		&& apt-get install -y \
		libbz2-dev \
		zlib1g-dev \
		&& docker-php-ext-install \
			zip \
			bz2

	# ftp
	RUN apt-get update \
		&& apt-get install -y \
		libssl-dev \
		&& docker-php-ext-install \
			ftp

	# ssh2
	RUN apt-get update \
		&& apt-get install -y \
		libssh2-1-dev

	# others
	RUN docker-php-ext-install \
		soap \
		sockets \
		sysvmsg \
		sysvsem \
		sysvshm

	# PECL
	RUN docker-php-pecl-install \
		ssh2-1.0 \
		redis-3.0 \
		apcu-5.1.5

	# Install XDebug, but not enable by default. Enable using:
	# * php -d$XDEBUG_EXT vendor/bin/phpunit
	# * php_xdebug vendor/bin/phpunit
	RUN pecl install xdebug-2.4.0
	ENV XDEBUG_EXT zend_extension=/usr/local/lib/php/extensions/no-debug-non-zts-20151012/xdebug.so
	RUN alias php_xdebug="php -d$XDEBUG_EXT vendor/bin/phpunit"

	# Install composer and put binary into $PATH
	RUN curl -sS https://getcomposer.org/installer | php \
		&& mv composer.phar /usr/local/bin/ \
		&& ln -s /usr/local/bin/composer.phar /usr/local/bin/composer

	# Install PHP Code sniffer
	RUN curl -OL https://squizlabs.github.io/PHP_CodeSniffer/phpcs.phar \
		&& chmod 755 phpcs.phar \
		&& mv phpcs.phar /usr/local/bin/ \
		&& ln -s /usr/local/bin/phpcs.phar /usr/local/bin/phpcs \
		&& curl -OL https://squizlabs.github.io/PHP_CodeSniffer/phpcbf.phar \
		&& chmod 755 phpcbf.phar \
		&& mv phpcbf.phar /usr/local/bin/ \
		&& ln -s /usr/local/bin/phpcbf.phar /usr/local/bin/phpcbf

	# Install PHPUnit
	RUN curl -OL https://phar.phpunit.de/phpunit.phar \
		&& chmod 755 phpunit.phar \
		&& mv phpunit.phar /usr/local/bin/ \
		&& ln -s /usr/local/bin/phpunit.phar /usr/local/bin/phpunit

	ADD php.ini /usr/local/etc/php/conf.d/docker-php.ini


## NodeJS, NPM
	ENV NVM_DIR /usr/local/nvm
	ENV NODE_VERSION 5.1.0

	# Install nvm with node and npm
	RUN curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.26.0/install.sh | bash \
    		&& . $NVM_DIR/nvm.sh \
    		&& nvm install $NODE_VERSION \
    		&& nvm alias default $NODE_VERSION \
    		&& nvm use default

	# Set up our PATH correctly so we don't have to long-reference npm, node, &c.
	ENV NODE_PATH $NVM_DIR/versions/node/v$NODE_VERSION/lib/node_modules
	ENV PATH      $NVM_DIR/versions/node/v$NODE_VERSION/bin:$PATH


# MariaDB
	RUN apt-get update \
		&& apt-get install -y software-properties-common \
		&& apt-key adv --recv-keys --keyserver keyserver.ubuntu.com 0xcbcb082a1bb943db \
		&& add-apt-repository 'deb [arch=amd64,i386] http://mirror.vpsfree.cz/mariadb/repo/10.1/debian jessie main'

	RUN apt-get update \
		&& apt-get install -y mariadb-server \
		&& mysql_install_db

	VOLUME /var/lib/mysql

	ADD my.cnf /etc/mysql/conf.d/my.cnf

	EXPOSE 3306


# Redis
	RUN apt-get update \
		&& apt-get install -y redis-server

	EXPOSE 6379


# Clean all
	RUN apt-get clean
	RUN rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* /var/cache/*
