FROM ubuntu:16.04

# Environment variables
ENV DEBIAN_FRONTEND noninteractive
ENV LC_ALL en_US.UTF-8
ENV LANGUAGE en_US:en

# Update package cache
RUN apt-get update -y --fix-missing
RUN apt-get -y dist-upgrade

# Install tools for package management/locales etc.
RUN apt-get -y --no-install-recommends install \
	wget \
	lsb-release \
	ca-certificates \
	curl \
	locales \
	apt-utils \
	gnupg \
	apt-transport-https \
	build-essential \
	python-software-properties \
	software-properties-common

# Set locale
RUN echo "en_US.UTF-8 UTF-8" >> /etc/locale.gen && locale-gen en_US.UTF-8 && /usr/sbin/update-locale LANG=en_US.UTF-8

# Source the ondrej PHP repository
RUN add-apt-repository -y -u ppa:ondrej/php && apt-get update

# Install PHP (7.2)
RUN apt-get -y --no-install-recommends install \
	php7.2-mysql \
	php7.2-mbstring \
	php7.2-opcache \
	php7.2-gd \
	php7.2-curl \
	php7.2-intl \
	php7.2-gettext \
	php7.2-json \
	php7.2-xml \
	php7.2-gd \
	php7.2-zip \
	php7.2-fpm \
	php7.2-memcached \
	php7.2-memcache \
	php-dev \
	php-pear

# Install ODBC stuff
RUN curl https://packages.microsoft.com/keys/microsoft.asc | apt-key add -
RUN curl https://packages.microsoft.com/config/ubuntu/16.04/prod.list | tee /etc/apt/sources.list.d/mssql-tools.list
RUN apt-get update
RUN ACCEPT_EULA=Y apt-get install -y msodbcsql unixodbc-dev

# Install over pecl
RUN pecl install sqlsrv pdo_sqlsrv
RUN echo "extension= pdo_sqlsrv.so" >> /etc/php/7.2/mods-available/pdo_sqlsrv.ini
RUN echo "extension= sqlsrv.so" >> /etc/php/7.2/mods-available/sqlsrv.ini
RUN ln -s /etc/php/7.2/mods-available/pdo_sqlsrv.ini /etc/php/7.2/fpm/conf.d/20-pdo_sqlsrv.ini
RUN ln -s /etc/php/7.2/mods-available/sqlsrv.ini /etc/php/7.2/fpm/conf.d/20-sqlsrv.ini
RUN ln -s /etc/php/7.2/mods-available/pdo_sqlsrv.ini /etc/php/7.2/cli/conf.d/20-pdo_sqlsrv.ini
RUN ln -s /etc/php/7.2/mods-available/sqlsrv.ini /etc/php/7.2/cli/conf.d/20-sqlsrv.ini

# Clean APT cache to save a bit of disk space
RUN apt-get autoclean && apt-get clean && apt-get autoremove

# Make php-fpm listen on port 9000
RUN sed -i -E "s/listen = .*/listen = [::]:9000/" /etc/php/7.2/fpm/pool.d/www.conf
RUN sed -i -E "s/;daemonize\s*=\s*yes/daemonize = no/g" /etc/php/7.2/fpm/php-fpm.conf

# Start PHP-FPM service
ENTRYPOINT service php7.2-fpm start && bash

# Expose port 9000
EXPOSE 9000
