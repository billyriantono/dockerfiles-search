FROM php:7.3-fpm

#install redis
RUN pecl install -o -f redis \
  &&  rm -rf /tmp/pear \
  &&  docker-php-ext-enable redis

#install pgsql
RUN apt-get update && apt-get install -y \
 	libpq-dev && \
	docker-php-ext-install \
	pdo \
	pdo_pgsql