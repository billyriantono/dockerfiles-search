FROM php:7.1.14-cli

RUN apt-get update

RUN buildDeps=" \
		libjpeg-dev \
		libmcrypt-dev \
		libpng12-dev \
		zlib1g-dev \
		libcurl4-gnutls-dev \
		libpq-dev \
		g++ libicu-dev \
	"; \
	set -x \
	&& apt-get update && apt-get install -y $buildDeps --no-install-recommends \
	&& docker-php-ext-configure gd --enable-gd-native-ttf \
	&& docker-php-ext-install gd \
	&& docker-php-ext-install mcrypt \
	&& docker-php-ext-install mysqli \
	&& docker-php-ext-install pdo_mysql \
	&& docker-php-ext-install zip \
	&& docker-php-ext-install bcmath \
	&& docker-php-ext-configure intl \
	&& docker-php-ext-install intl \
	&& apt-get purge -y --auto-remove $buildDeps

RUN apt-get update && apt-get install -y git ssh mysql-client libmcrypt4 libpq5 sendmail libicu-dev --no-install-recommends && rm -rf /var/lib/apt/lists/*

RUN apt-get update -yqq && apt-get install libxml2-dev -yqq && docker-php-ext-install soap xml

# composer install
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer
