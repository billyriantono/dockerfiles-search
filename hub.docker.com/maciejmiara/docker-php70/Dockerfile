FROM ubuntu:xenial

MAINTAINER Maciej Miara <mkowalski8@gmail.com>

ENV DEBIAN_FRONTEND noninteractive

# Install dependencies
RUN apt-get update && apt-get install -y --no-install-recommends \
      ca-certificates \
	  vim \
      curl \
      php7.0 \
      php7.0-cli \
	  php7.0-bcmath \
	  php7.0-curl \
	  php7.0-intl \
	  php7.0-mcrypt \
	  php7.0-mysql \
	  php7.0-pgsql \
	  php-memcached \
	  php7.0-mbstring \
	  php7.0-zip \
	  php7.0-xml \
    && rm -rf /var/lib/apt/lists/*

# Configure PHP-FPM
RUN echo "opcache.enable=1" >> /etc/php/7.0/mods-available/opcache.ini \
    && echo "opcache.enable_cli=1" >> /etc/php/7.0/mods-available/opcache.ini \
	&& echo "date.timezone = UTC" >> /etc/php/7.0/cli/php.ini
	
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

EXPOSE 8000-8080
