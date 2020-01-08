FROM php:5.6-fpm-alpine

RUN	set -x \ 
	delgroup www-data \
	&& deluser www-data \
	&& addgroup -g 1008 -S www-data \
	&& adduser -u 1008 -D -S -G www-data www-data

RUN 	apk add --no-cache --update imagemagick-dev libmcrypt-dev libmcrypt make gcc g++ \ 
	icu-dev libcurl curl-dev libxslt-dev openldap-dev \
	libpng \
	imagemagick \
	c-client \
	icu-libs \
	libldap \
	libxslt \
	krb5-libs \
	libxml2-dev \
	openssl-dev \
	bzip2-dev \
	jpeg-dev \
	libpng-dev \
	libxpm-dev \
	freetype-dev \
	gettext-dev \
	gmp-dev \
	imap-dev \
	krb5-dev \
	icu-dev \
	freetds-dev \
	enchant-dev \
	aspell-dev \
	readline-dev \
	libedit-dev \
	net-snmp-dev \
	libxslt-dev \
	db-dev \
	gdbm-dev \
	build-base \
	autoconf \
	libtool \
	geoip \
	geoip-dev \
	&& docker-php-ext-install iconv \
	&& docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
	&& docker-php-ext-install  gd \
	&& docker-php-ext-configure imap --with-kerberos --with-imap-ssl \
	&& docker-php-ext-install imap \
	&& docker-php-ext-install intl \
	&& docker-php-ext-configure intl \
	&& docker-php-ext-install curl \
        && docker-php-ext-configure mcrypt \
	&& docker-php-ext-install mcrypt \
	&& docker-php-ext-install xsl \
	&& docker-php-ext-install ldap \
	&& docker-php-ext-install mysqli \
	&& docker-php-ext-install opcache \
	&& docker-php-ext-install soap \
	&& docker-php-ext-install pdo pdo_mysql \
	&& docker-php-ext-install xsl \
	&& pecl install imagick \
	&& pecl install geoip \
	&& pecl install memcache \
	&& pecl install redis \
	&& pecl install xdebug \
	&& docker-php-ext-enable imagick \
	&& docker-php-ext-enable geoip \
	&& docker-php-ext-enable memcache \
	&& docker-php-ext-enable redis \
	&& docker-php-ext-enable xdebug

RUN 	apk del imagemagick-dev libmcrypt-dev make gcc g++ \ 
	icu-dev curl-dev libxslt-dev openldap-dev \
	libxml2-dev \
	openssl-dev \
	bzip2-dev \
	jpeg-dev \
	libpng-dev \
	libxpm-dev \
	freetype-dev \
	gettext-dev \
	gmp-dev \
	imap-dev \
	krb5-dev \
	icu-dev \
	freetds-dev \
	enchant-dev \
	aspell-dev \
	readline-dev \
	libedit-dev \
	net-snmp-dev \
	libxslt-dev \
	db-dev \
	gdbm-dev \
	build-base \
	autoconf 

ADD	php.ini /usr/local/etc/php/php.ini

