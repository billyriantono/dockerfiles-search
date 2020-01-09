FROM php:7.1.6-fpm

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

RUN apt-get update \
	&& apt-get install -y \
		openssl \
		git

RUN apt-get update \
	&& apt-get install -y libicu-dev \
	&& docker-php-ext-configure intl \
	&& docker-php-ext-install intl

RUN apt-get update \
	&& apt-get install -y \
		libxml2-dev \
		libxslt-dev \
	&& docker-php-ext-install \
		dom \
		xmlrpc \
		xsl

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

RUN docker-php-ext-install \
	mysqli \
	pdo \
	pdo_mysql

RUN apt-get update \
	&& apt-get install -y libmcrypt-dev \
	&& docker-php-ext-install mcrypt

RUN docker-php-ext-install \
	gettext \
	mbstring

RUN apt-get update \
	&& apt-get install -y \
		libbz2-dev \
		zlib1g-dev \
	&& docker-php-ext-install \
		zip \
		bz2

RUN apt-get update \
	&& apt-get install -y libssl-dev \
	&& docker-php-ext-install \
		ftp

RUN apt-get update \
	&& apt-get install -y libssh2-1-dev

RUN git clone https://github.com/php/pecl-networking-ssh2.git /usr/src/php/ext/ssh2 \
	&& docker-php-ext-install ssh2
	
RUN docker-php-ext-install opcache

RUN { \
	echo 'opcache.memory_consumption=128'; \
	echo 'opcache.interned_strings_buffer=8'; \
	echo 'opcache.max_accelerated_files=4000'; \
	echo 'opcache.revalidate_freq=60'; \
	echo 'opcache.fast_shutdown=1'; \
	echo 'opcache.enable_cli=1'; \
	} > /usr/local/etc/php/conf.d/opcache-recommended.ini

RUN echo "realpath_cache_size = 4096k; realpath_cache_ttl = 7200;" > /usr/local/etc/php/conf.d/php.ini
