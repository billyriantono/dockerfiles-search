FROM php:7.2-fpm-alpine

# Install git
RUN apk update
RUN apk add --no-cache git

# install composer
RUN curl -sS https://getcomposer.org/installer | php
RUN mv composer.phar /usr/local/bin/composer

# Goto temporary directory.
WORKDIR /tmp

# Run composer and phpunit installation.
RUN composer selfupdate && \
  composer require "phpunit/phpunit:~5.4" && \
  ln -s /tmp/vendor/bin/phpunit /usr/local/bin/phpunit


# Set up the application directory.
VOLUME ["/app"]
WORKDIR /app