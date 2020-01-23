# Docker image specification for Apache and PHP for Drupal.
#
# - Download and enable the following PHP extensions:
#   - uploadprogress - https://pecl.php.net/package/uploadprogress
#   - memcache - https://pecl.php.net/package/memcache
#   - gd
#       - also libpng12-dev, libjpeg62-turbo-dev, libfreetype6-dev required from apt
#   - mcrypt
#       - also libmcrypt-dev required from apt
#   - pdo_mysql, mbstring, zip and opcache
# - Add Apache configuration and enable mod_rewrite.
#
# VERSION 0.4

FROM php:5.6.10-apache
MAINTAINER Aleksi Johansson <aleksi@aleksijohansson.net>

# Put the helper script into place.
COPY provisioning/move.sh /usr/local/bin/move

RUN \
# Update apt-get cache.
apt-get update \
# Install gd dependencies.
&& apt-get install -y libpng12-dev libjpeg62-turbo-dev libfreetype6-dev \
# Install mcrypt dependencies.
&& apt-get install -y libmcrypt-dev \
# Download the Memcache extension for PHP.
&& cd /usr/src/php/ext \
&& pecl download memcache-3.0.8 \
&& gzip -d < memcache-3.0.8.tgz | tar -xvf - \
&& rm memcache-3.0.8.tgz \
&& mv memcache-3.0.8 memcache \
# Download the uploadprogress extension for PHP.
&& pecl download uploadprogress \
# Use helper script to rename the uploadprogress extension.
&& move f uploadprogress uploadprogress.tgz \
&& gzip -d < uploadprogress.tgz | tar -xvf - \
&& rm uploadprogress.tgz \
# Use helper script to rename the uploadprogress extension.
&& move d uploadprogress uploadprogress \
# Install Drupal required PHP extensions.
&& docker-php-ext-install pdo_mysql mbstring zip opcache mcrypt memcache gd uploadprogress

# Put the Apache configuration into place.
COPY provisioning/apache2.conf /etc/apache2/apache2.conf

# Enable Apache mod_rewrite.
RUN a2enmod rewrite
