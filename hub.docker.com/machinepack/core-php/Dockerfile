FROM php:7.0

RUN apt-get update \
	&& apt-get install -y \
		unzip \
		git \
		libxml2-dev \
	&& apt-get clean -y

RUN pear install soap-beta \
	&& docker-php-ext-install soap

RUN curl -sS https://getcomposer.org/installer \
	| php -- --install-dir=/usr/local/bin --filename=composer
