FROM php:7.0-apache

RUN a2enmod rewrite include

# Install extension
RUN apt-get update \
	&& apt-get install -y \
	libbz2-dev \
	libxml2-dev \
	zlib1g-dev \
	libfreetype6-dev \
	libjpeg62-turbo-dev \
	libmcrypt-dev \
	libpng12-dev \
	libgmp-dev \
	libedit-dev \
	libreadline6-dev \
	libxslt-dev
RUN ln -s /usr/include/x86_64-linux-gnu/gmp.h /usr/include/gmp.h && \
	docker-php-ext-install bcmath bz2 calendar exif gettext pdo_mysql readline shmop soap sockets sysvmsg sysvsem sysvshm wddx zip opcache gmp mcrypt xsl \
	&& docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
	&& docker-php-ext-install -j$(nproc) gd

# Install xdebug
RUN pecl install xdebug && \
	echo "zend_extension=/usr/local/lib/php/extensions/no-debug-non-zts-20151012/xdebug.so" > /usr/local/etc/php/conf.d/xdebug.ini && \
	echo "extension=readline.so" > /usr/local/etc/php/conf.d/docker-php-ext-readline.ini
