FROM php:7.2-cli-stretch

RUN apt-get update; \
	apt-get install -y --no-install-recommends \
	zlib1g-dev \
	libpng-dev \
	git \
	ssh \
	rsync \
	wget \
	&& docker-php-ext-install zip \
	&& docker-php-ext-install gd \ 
	&& docker-php-ext-install sockets \
	&& docker-php-ext-install bcmath \
	&& docker-php-ext-configure bcmath --enable-bcmath

# Install composer

RUN curl -sS https://getcomposer.org/installer | php
RUN mv composer.phar /usr/local/bin/composer

# Install WP-CLI for wordpress

RUN curl -O https://raw.githubusercontent.com/wp-cli/builds/gh-pages/phar/wp-cli.phar
RUN chmod +x wp-cli.phar
RUN mv wp-cli.phar /usr/local/bin/wp

WORKDIR /tmp

RUN composer require "phpunit/phpunit:~5.3.4" --prefer-source --no-interaction && \
    ln -s /tmp/vendor/bin/phpunit /usr/local/bin/phpunit

RUN phpunit --version

CMD ["php", "-a"]