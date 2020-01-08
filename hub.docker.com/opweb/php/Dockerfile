FROM php:7.1-apache

RUN a2enmod rewrite

RUN apt-get update
RUN apt-get install -y git zlib1g-dev --no-install-recommends

RUN apt-get update -y
RUN apt-get install -y \
        libicu-dev \
        libmcrypt-dev \
        libpq-dev \
	libxml2-dev \
        libfreetype6-dev \
        libjpeg62-turbo-dev \
        libmcrypt-dev \
        libc-client-dev libkrb5-dev \
	python-dev \
	openssh-client \
	unzip \
        && rm -rf /var/lib/apt/lists/*

RUN docker-php-ext-install pdo pdo_mysql xml mysqli intl mbstring zip bcmath

RUN docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
    && docker-php-ext-install gd

RUN docker-php-ext-configure imap --with-kerberos --with-imap-ssl && \
        docker-php-ext-install -j$(nproc) imap

# Install composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

# Install XDebug
RUN yes | pecl install xdebug \
      && echo "zend_extension=$(find /usr/local/lib/php/extensions/ -name xdebug.so)" > /usr/local/etc/php/conf.d/xdebug.ini \
      && echo "xdebug.profiler_enable = 0" >> /usr/local/etc/php/conf.d/xdebug.ini \
      && echo "xdebug.profiler_enable_trigger = 1" >> /usr/local/etc/php/conf.d/xdebug.ini \
      && echo "xdebug.default_enable = 0" >> /usr/local/etc/php/conf.d/xdebug.ini \
      && echo "xdebug.remote_enable=1" >> /usr/local/etc/php/conf.d/xdebug.ini \
      && echo "xdebug.remote_port=9000" >> /usr/local/etc/php/conf.d/xdebug.ini \
      && echo "xdebug.remote_host=192.168.0.1" >> /usr/local/etc/php/conf.d/xdebug.ini \
      && echo "xdebug.idekey=phpstorm" >> /usr/local/etc/php/conf.d/xdebug.ini \
      && echo "xdebug.remote_autostart=1" >> /usr/local/etc/php/conf.d/xdebug.ini
