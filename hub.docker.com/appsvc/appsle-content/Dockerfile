FROM php:7.2-apache

# Dev Utils
RUN apt-get update && apt-get install -y \
	git \
	vim \
	unzip \
	zip \
        curl

# PHP Extensions
RUN apt-get -y install libtidy-dev \
    && docker-php-ext-install tidy

RUN apt-get install -y zlib1g-dev \
    && docker-php-ext-install zip

WORKDIR /var/www/html

# Add composer
RUN curl -sS https://getcomposer.org/installer | php \
    && mv composer.phar /usr/bin/composer

# Update virtual host configuration
ADD config/appizy-vhost.conf /etc/apache2/sites-enabled/vhost-appizy.conf

RUN rm /etc/apache2/sites-enabled/000-default.conf

# Enable Apache modules
RUN a2enmod rewrite
RUN a2enmod headers

# Allow the application to write files 
RUN usermod -u 1000 www-data
RUN usermod -G staff www-data

# Install xdebug RUN pecl channel-update pecl.php.net
RUN pecl install xdebug-2.7.2
RUN echo 'zend_extension = /usr/local/lib/php/extensions/no-debug-non-zts-20131226/xdebug.so' >> /usr/local/etc/php/php.ini
RUN touch /usr/local/etc/php/conf.d/xdebug.ini; \
    echo xdebug.remote_enable=1 >> /usr/local/etc/php/conf.d/xdebug.ini; \
    echo xdebug.remote_autostart=0 >> /usr/local/etc/php/conf.d/xdebug.ini; \
    echo xdebug.remote_connect_back=1 >> /usr/local/etc/php/conf.d/xdebug.ini; \
    echo xdebug.remote_port=9000 >> /usr/local/etc/php/conf.d/xdebug.ini; \
    echo xdebug.remote_log=/tmp/php5-xdebug.log >> /usr/local/etc/php/conf.d/xdebug.ini;

# Timezone
RUN echo 'date.timezone = Europe/Berlin' > /usr/local/etc/php/conf.d/date.ini
