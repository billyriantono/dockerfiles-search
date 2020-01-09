FROM php:7.4-cli-alpine

RUN apk update \
	&& docker-php-ext-install bcmath \
	&& docker-php-ext-install pdo_mysql