FROM php:5.6-fpm

LABEL version="1.0"

RUN apt-get update -y && \
	apt-get install -y mysql-client && \
	apt-get install -y git
RUN apt-get install -y libmcrypt-dev  libzip-dev

# Install required PHP dependencies
RUN docker-php-ext-install mysql pdo_mysql json bcmath tokenizer mbstring mcrypt zip 

# Use Custom PHP.ini configuration
COPY config/php.ini /usr/local/etc/php/

# Install Composer
RUN curl -sS https://getcomposer.org/installer | php && \
	mv composer.phar /usr/local/bin/composer

# Github Token
RUN composer global config github-oauth.github.com 9236becd6d8d4ff01e29874597ee7b6e96abb7a5

# Install Laravel command
RUN composer global require "laravel/installer=~1.1"
RUN composer global require "phpunit/phpunit=4.3.*"

# Add Laravel Binary to PATH
CMD ["export PATH=/root/.composer/vendor/bin:$PATH"]

COPY config/php.sh /php.sh
RUN chmod +x /php.sh

ENTRYPOINT ["/php.sh"]
