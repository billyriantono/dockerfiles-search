FROM php:5.6-apache
MAINTAINER Sébastien SERRE <sebastien@thivinfo.com>

# fix osx permissions
RUN usermod -u 1000 www-data
RUN groupmod -g 1000 www-data
RUN a2enmod rewrite

RUN apt-get update && \
	apt-get install -y --no-install-recommends \

# For bz2

		libbz2-dev \

# For gd

		libfreetype6-dev \
		libjpeg62-turbo-dev \
		libpng12-dev \
		libxpm-dev \
		libvpx-dev \

# For ftp

		libssl-dev \

# For mcrypt

		libmcrypt-dev \

# For memcached

		libmemcached-dev \
	&& \

# Cleanup

	apt-get clean && \
	rm -rf /var/lib/apt/lists/* && \

# Configure GD package for JPEG support

	docker-php-ext-configure gd \
		--with-freetype-dir=/usr/lib/x86_64-linux-gnu/ \
		--with-jpeg-dir=/usr/lib/x86_64-linux-gnu/ \
		--with-xpm-dir=/usr/lib/x86_64-linux-gnu/ \
		--with-vpx-dir=/usr/lib/x86_64-linux-gnu/ \
	&& \

# Install some extra PHP Extension

	docker-php-ext-install \
		bcmath \
		bz2 \
		exif \
		ftp \
		gd \
		gettext \
		mbstring \
		mcrypt \
		mysqli \
		opcache \
		pdo_mysql \
		shmop \
		sockets \
		sysvmsg \
		sysvsem \
		sysvshm \
		zip \
	&& \

# Some extensions need to be installed via PECL

	pecl install apcu-4.0.8 memcached && \
	echo 'extension = apcu.so' > /usr/local/etc/php/conf.d/apcu.ini && \
	echo 'extension = memcached.so' > /usr/local/etc/php/conf.d/memcached.ini

# php5 apache2 stuff

COPY ./php.ini /usr/local/etc/php/php.ini

RUN echo "ServerName localhost" >>/etc/apache2/apache2.conf

RUN touch /usr/local/etc/php/conf.d/php.ini \
    && echo "memory_limit  = 128M" >> /usr/local/etc/php/conf.d/php.ini \
    && echo "upload_max_filesize = 64M" >> /usr/local/etc/php/conf.d/php.ini \
    && echo "post_max_size = 64M" >> /usr/local/etc/php/conf.d/php.ini \
    && echo "error_reporting = E_ALL" >> /usr/local/etc/php/conf.d/php.ini \
    && echo "display_errors = On" >> /usr/local/etc/php/conf.d/php.ini \
    && echo "date.timezone = Europe/Paris" >> /usr/local/etc/php/conf.d/php.ini

# xdebug
RUN yes | pecl install xdebug \
    && echo "zend_extension=$(find /usr/local/lib/php/extensions/ -name xdebug.so)" > /usr/local/etc/php/conf.d/xdebug.ini \
    && echo "xdebug.remote_enable=on" >> /usr/local/etc/php/conf.d/xdebug.ini \
    && echo "xdebug.remote_autostart=off" >> /usr/local/etc/php/conf.d/xdebug.ini

VOLUME /var/www/html

CMD ["apache2-foreground"]
