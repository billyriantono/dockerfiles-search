FROM composer:latest

RUN apk update && apk add \
    libmemcached-dev \
    zip \
    libzip-dev \
    libpng-dev \
    freetype-dev \
    libjpeg-turbo-dev \
    libxml2-dev

RUN docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ --with-png-dir=/usr/include/ && \
	docker-php-ext-configure bcmath && \
	docker-php-ext-configure zip --with-libzip && \
	docker-php-ext-install gd \
						   pdo_mysql \
						   mbstring \
						   zip \
						   bcmath \
						   soap \
						   sockets \
						   mysqli \
						   xmlrpc \
						   xml