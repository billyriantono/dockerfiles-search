FROM php:7.2-fpm

RUN apt-get update
RUN apt-get install -y --no-install-recommends \
	apt-utils \
	git \
	libssl-dev \
	nginx \
	vim \
	wget \
	zlib1g-dev && \
	EXPECTED_COMPOSER_SIGNATURE=$(wget -q -O - https://composer.github.io/installer.sig) && \
	php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');" && \
	php -r "if (hash_file('SHA384', 'composer-setup.php') === '${EXPECTED_COMPOSER_SIGNATURE}') { echo 'Composer.phar Installer verified'; } else { echo 'Composer.phar Installer corrupt'; unlink('composer-setup.php'); } echo PHP_EOL;" && \
	php composer-setup.php --install-dir=/usr/bin --filename=composer && \
	php -r "unlink('composer-setup.php');" && \
	pecl install mongodb-1.5.2 && \
	docker-php-ext-install pdo pdo_mysql zip && \
	docker-php-ext-enable mongodb
RUN apt-get remove -y wget libssl-dev zlib1g-dev && \
	apt-get clean

# Custom config files
COPY src/becausecode.ini /usr/local/etc/php/

WORKDIR /var/www
