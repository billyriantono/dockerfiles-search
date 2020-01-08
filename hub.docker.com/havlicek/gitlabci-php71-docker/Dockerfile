FROM php:7.1

MAINTAINER Michal Havlicek <michalhavlicek.com@gmail.com>

# Install git (the php image doesn't have it) which is required by composer
RUN apt-get update -yqq \
    && apt-get install -yqq git \
        zlib1g-dev

# Install mysql driver
RUN docker-php-ext-install pdo_mysql
RUN docker-php-ext-install zip

# Install phpunit, the tool that we will use for testing
RUN curl --location --output /usr/local/bin/phpunit https://phar.phpunit.de/phpunit.phar && chmod +x /usr/local/bin/phpunit

# Install composer
RUN curl --silent --show-error https://getcomposer.org/installer | php && mv composer.phar /usr/local/bin/composer
