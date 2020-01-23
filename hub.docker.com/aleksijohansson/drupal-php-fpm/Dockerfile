# Docker image specification for PHP-FPM for Drupal.
#
# - Download and enable the following PHP extensions:
#   - uploadprogress - https://pecl.php.net/package/uploadprogress
#   - memcache - https://pecl.php.net/package/memcache
#   - gd
#       - also libpng12-dev, libjpeg62-turbo-dev, libfreetype6-dev required from apt
#   - mcrypt
#       - also libmcrypt-dev required from apt
#   - pdo_mysql, mbstring, zip and opcache
#
# VERSION 0.6

FROM php:5.6.11-fpm
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
# Configure gd to add freetype and jpeg support.
&& docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
# Install Drupal required PHP extensions.
&& docker-php-ext-install pdo_mysql mbstring zip opcache mcrypt memcache gd uploadprogress

# Put PHP-FPM configuration into place.
COPY provisioning/php-fpm-min.conf /usr/local/etc/php-fpm.conf
