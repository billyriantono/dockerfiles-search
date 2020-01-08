# Pull base image.
FROM php:7.2-fpm

# Update apt registry
RUN apt-get update || apt-get update

# Installation of needed extensions.
RUN apt-get install --fix-missing -y \
  apt-transport-https \
  apt-utils \
  imagemagick \
  graphviz \
	gnupg \
  libicu-dev \
  libmemcached-tools \
  libmemcached-dev \
  libpng-dev \
  libjpeg62-turbo-dev \
  libmcrypt-dev \
  libxml2-dev \
  libxslt1-dev \
  libyaml-dev \
  linux-libc-dev \
  mysql-client \
  ruby-dev \
  rubygems \
  sudo \
	wget \
  zip

RUN chmod +x /usr/local/bin/docker-php-ext-install
RUN docker-php-ext-configure gd --with-jpeg-dir=/usr/include/ \
&& docker-php-ext-install \
  calendar \
  exif \
  gd \
  intl \
  opcache \
  pdo_mysql \
  soap \
  xsl \
  zip

# Installation of Composer
RUN cd /usr/src && curl -sS http://getcomposer.org/installer | php
RUN cd /usr/src && mv composer.phar /usr/bin/composer

# pecl will claim success even if one install fails, so we need to perform each install separately
RUN pecl install APCu-5.1.11; \
	pecl install memcached-3.0.4; \
	pecl install redis-4.1.1;

RUN	docker-php-ext-enable \
		apcu \
		memcached \
		redis;

# Give ownership of the /var/www/html to www-data users
RUN chown www-data:root /var/www -R

# installation of ssmtp @todo:debug
RUN DEBIAN_FRONTEND=noninteractive apt-get install --fix-missing -y ssmtp
ADD config/ssmtp.conf /etc/ssmtp/ssmtp.conf
ADD config/php-smtp.ini /usr/local/etc/php/conf.d/php-smtp.ini

# Installation of Opcode cache
RUN ( \
  echo "opcache.memory_consumption=128"; \
  echo "opcache.interned_strings_buffer=8"; \
  echo "opcache.max_accelerated_files=12000"; \
  echo "opcache.revalidate_freq=2"; \
  echo "opcache.fast_shutdown=1"; \
  echo "opcache.enable_cli=1"; \
  ) > /usr/local/etc/php/conf.d/opcache-recommended.ini

