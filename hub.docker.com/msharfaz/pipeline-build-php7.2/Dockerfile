FROM php:7.2.25-apache

# Update Ubuntu Software repository and install necessary softwares
RUN apt-get update \
    && apt-get install -y \
        procps \
        openssh-client \
        rsync \
        curl \
        git \
        unzip \
        libxslt-dev \
        gnupg2 \
        wget \
        libicu-dev \
        zlib1g-dev \
        libzip-dev \
        libpng-dev \
    && docker-php-ext-install xsl opcache intl zip gd

# Node.js
RUN apt-get remove cmdtest

ENV NODE_VERSION=8.x
RUN set -xe; \
	curl -fsSL https://deb.nodesource.com/gpgkey/nodesource.gpg.key | apt-key add -; \
	echo "deb https://deb.nodesource.com/node_${NODE_VERSION} jessie main" | tee /etc/apt/sources.list.d/nodesource.list; \
	echo "deb-src https://deb.nodesource.com/node_${NODE_VERSION} jessie main" | tee -a /etc/apt/sources.list.d/nodesource.list; \
	curl -fsSL https://dl.yarnpkg.com/debian/pubkey.gpg | apt-key add -; \
	echo "deb https://dl.yarnpkg.com/debian/ stable main" | tee /etc/apt/sources.list.d/yarn.list; \
	apt-get update >/dev/null; \
	apt-get -y --no-install-recommends install >/dev/null \
		nodejs \
		npm \
		yarn

## Run yarn globally in case if not installed
RUN npm install -g yarn

## Install Composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/bin --filename=composer

# Install PHPUnit
RUN cd /tmp && curl https://phar.phpunit.de/phpunit.phar > phpunit.phar && \
    chmod +x phpunit.phar && \
    mv /tmp/phpunit.phar /usr/local/bin/phpunit

## Install Deployer with recipes
RUN composer global require deployer/deployer:6.6.0
RUN composer global require deployer/recipes --dev

# Ensure UTF-8
ENV LANG       en_US.UTF-8
ENV LC_ALL     en_US.UTF-8

## Add Composer vendor into PATH
ENV PATH /root/.composer/vendor/bin:$PATH