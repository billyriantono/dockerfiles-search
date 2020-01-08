FROM php:7.3-apache
MAINTAINER Chris Ewing <chris@alltiersolutions.com>

# Set Composer version to install
ENV COMPOSER_VERSION 1.9.1

# Set Drush version to install
#ENV DRUSH_VERSION 8.1.18

RUN apt-get update && apt-get install -y \
       git \
       libpng-dev \
       mariadb-client \
       unzip \
  # Install php extensions
    && docker-php-ext-install gd mysqli opcache pdo_mysql \
  # Enable apache modules
    && a2enmod rewrite \
  # Install Drush version specified above
  #  && curl -fsSL -o /usr/local/bin/drush "https://github.com/drush-ops/drush/releases/download/$DRUSH_VERSION/drush.phar" \
  #  && chmod +x /usr/local/bin/drush
  # Install the composer version specified above
    && curl -o /usr/local/bin/composer "https://getcomposer.org/download/$COMPOSER_VERSION/composer.phar" \
    && chmod +x /usr/local/bin/composer

COPY etc/php/ /usr/local/etc/php/

EXPOSE 80
