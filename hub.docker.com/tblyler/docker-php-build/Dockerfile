FROM php:latest
LABEL maintainer "Tony Blyler <me@tonyblyler.com>"

RUN pecl install xdebug && \
	docker-php-ext-install pcntl sockets && \
	docker-php-ext-enable xdebug && \
	apt-get update && \
	apt-get install -y \
		git \
		wget \
		openssh-client

ENTRYPOINT ["docker-php-entrypoint"]
CMD ["php", "-a"]
