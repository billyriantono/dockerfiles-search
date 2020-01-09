FROM library/php:fpm-alpine

RUN apk add --no-cache autoconf gcc g++ imagemagick-dev libtool make libxml2-dev \
    && pecl install imagick \
    && docker-php-ext-enable imagick \
    && pecl install xdebug-beta \
    && docker-php-ext-enable xdebug \
    && docker-php-ext-install xml \
    && docker-php-ext-install mysqli \
	&& docker-php-ext-install pdo \
	&& docker-php-ext-install pdo_mysql \
	&& docker-php-ext-install pcntl \
	&& docker-php-ext-install mbstring \
	&& docker-php-ext-install calendar \
	&& docker-php-ext-install tokenizer \
	&& apk del autoconf g++ libtool make \
