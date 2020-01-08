FROM php:7.2-cli

RUN docker-php-ext-install pcntl \ 
	&& pecl install xdebug \
	&& docker-php-ext-enable xdebug
 
