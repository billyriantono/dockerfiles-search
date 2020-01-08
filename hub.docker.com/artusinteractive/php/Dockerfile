FROM php:7.0-apache

MAINTAINER Michael Petri <mpetri@artus.com>

# enable apache modules
RUN a2enmod rewrite

# install the PHP extensions we need
RUN apt-get update && apt-get install -y libpng12-dev libjpeg-dev libpq-dev \
	&& rm -rf /var/lib/apt/lists/* \
	&& docker-php-ext-configure gd --with-png-dir=/usr --with-jpeg-dir=/usr \
	&& docker-php-ext-install gd mbstring opcache pdo pdo_mysql pdo_pgsql zip
RUN yes | pecl install xdebug

# set recommended PHP.ini settings
# see https://secure.php.net/manual/en/opcache.installation.php
RUN { \
		echo 'opcache.memory_consumption=128'; \
		echo 'opcache.interned_strings_buffer=8'; \
		echo 'opcache.max_accelerated_files=4000'; \
		echo 'opcache.revalidate_freq=60'; \
		echo 'opcache.fast_shutdown=1'; \
		echo 'opcache.enable_cli=1'; \
	} > $PHP_INI_DIR/conf.d/opcache-recommended.ini
RUN { \
        echo "zend_extension=$(find /usr/local/lib/php/extensions/ -name xdebug.so)"; \
        echo 'xdebug.remote_enable = 1'; \
        echo 'xdebug.remote_connect_back = 1'; \
        echo 'xdebug.remote_autostart = 1'; \
	} > $PHP_INI_DIR/conf.d/xdebug-recommended.ini

ENV APACHE_DOCROOT /var/www/html
RUN sed -i -e 's@/var/www/html@${APACHE_DOCROOT}@g' /etc/apache2/sites-enabled/000-default.conf