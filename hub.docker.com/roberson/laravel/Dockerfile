FROM php:7.0-apache

# Increase memory limit
RUN echo "memory_limit=4096M" > $PHP_INI_DIR/conf.d/memory-limit.ini

# Install modules
RUN apt-get update && apt-get install -y \
        git \
        libssl-dev \
        libfreetype6-dev \
        libjpeg62-turbo-dev \
        libmcrypt-dev \
        libpng12-dev \
	libxml2-dev \
	libpq-dev \
	node \
	npm
RUN docker-php-ext-configure pgsql -with-pgsql=/usr/local/pgsql
RUN docker-php-ext-install mbstring tokenizer pcntl pdo pdo_mysql pdo_pgsql pgsql bcmath
RUN docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/
RUN docker-php-ext-install gd zip

# Install pecl extensions
RUN pecl install mongodb-1.2.0alpha1 \
    && pecl install xdebug
RUN docker-php-ext-enable xdebug mongodb
RUN docker-php-ext-install soap

# Install composer
RUN curl -sS https://getcomposer.org/installer \
        | php -- --install-dir=/usr/local/bin \
        && mv /usr/local/bin/composer.phar /usr/local/bin/composer

# Configure apache
RUN sed -i "s/DocumentRoot .*/DocumentRoot \/var\/www\/public/" /etc/apache2/sites-enabled/000-default.conf
RUN echo "error_reporting = E_ALL & ~E_DEPRECATED & ~E_STRICT" >> /usr/local/etc/php/conf.d/error.ini
RUN echo "log_errors = On" >> /usr/local/etc/php/conf.d/error.ini
RUN echo "KeepAlive On" >> /etc/apache2/conf-enabled/keep-alive.conf
RUN echo "KeepAliveTimeout 75" >> /etc/apache2/conf-enabled/keep-alive.conf
RUN a2enmod rewrite
RUN a2enmod headers

# Configure task scheduling
RUN apt-get install -y cron
RUN echo "* * * * *   root    php /var/www/artisan schedule:run >> /dev/null 2>&1" >> /etc/crontab

RUN echo "zend_extension=$(find /usr/local/lib/php/extensions/ -name xdebug.so)" > /usr/local/etc/php/conf.d/xdebug.ini \
    && echo "xdebug.remote_enable=on" >> /usr/local/etc/php/conf.d/xdebug.ini \
    && echo "xdebug.remote_autostart=off" >> /usr/local/etc/php/conf.d/xdebug.ini

# Set storage to writable
COPY . /var/www/
WORKDIR /var/www/
