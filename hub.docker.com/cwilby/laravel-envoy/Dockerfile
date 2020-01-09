FROM php:latest
LABEL maintainer="cameron@wilby.com"

RUN apt-get update -yqq
RUN apt-get install gnupg1 gnupg2 -yqq
RUN curl -sL https://deb.nodesource.com/setup_8.x | bash -
RUN apt-get install git \
	nodejs \
	libcurl4-gnutls-dev \
	libicu-dev \
	libmcrypt-dev \
	libvpx-dev \
	libjpeg-dev \
	libpng-dev \
	libxpm-dev \
	zlib1g-dev \
	libfreetype6-dev \
	libxml2-dev \
	libexpat1-dev \
	libbz2-dev \
	libgmp3-dev \
	libldap2-dev \
	unixodbc-dev \
	libpq-dev \
	libsqlite3-dev \
	libaspell-dev \
	libsnmp-dev \
	libpcre3-dev \
	libtidy-dev \
	-yqq

RUN apt-get update && apt-get install -y curl apt-transport-https && \
    curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | apt-key add - && \
    echo "deb https://dl.yarnpkg.com/debian/ stable main" | tee /etc/apt/sources.list.d/yarn.list && \
    apt-get update && apt-get install -y yarn
    
RUN pecl install mcrypt-1.0.1
RUN docker-php-ext-enable mcrypt

RUN docker-php-ext-install mbstring \
	pdo_mysql \
	curl \
	json \
	intl \
	gd \
	xml \
	zip \
	bz2 \
	opcache

RUN curl --location --output /usr/local/bin/phpunit https://phar.phpunit.de/phpunit.phar
RUN chmod +x /usr/local/bin/phpunit

ENV COMPOSER_HOME=/composer
ENV COMPOSER_ALLOW_SUPERUSER=1
ENV PATH $COMPOSER_HOME/vendor/bin:$PATH

RUN mkdir /composer \
    && curl -sS https://getcomposer.org/installer | php \
    && mkdir -p /opt/composer \
    && mv composer.phar /usr/bin/composer
    
RUN composer global require laravel/envoy