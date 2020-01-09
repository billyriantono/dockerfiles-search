###############################################################################
# Laravel dev/test Environment (v0.1)
#
# Required software:
#	- PHP 7.0.15
#	- Composer 1.4.1
#	- Node 6.10.2 (6.X LTS)
#	- NPM 3.10.10
###############################################################################

FROM ubuntu:xenial

# Setup
RUN apt-get -y update && apt-get -y upgrade
RUN apt-get install -y curl \
    git \
	zip unzip

# Install PHP extensions and tools
RUN apt-get install -y php7.0-cli \
	php-curl \
	php-mcrypt \
	php-mbstring \
	php-gettext \
	php-gd \
	php7.0-sqlite3

# Install Composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

# Install NodeJS & NPM
RUN curl -sL https://deb.nodesource.com/setup_6.x | bash -
RUN apt-get install -y nodejs
