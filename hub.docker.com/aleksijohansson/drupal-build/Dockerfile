# Docker image specification for build.sh for Drupal.
#
# - Add new user called bro to run PHP with.
# - Download and enable the following PHP extensions:
#   - uploadprogress - https://pecl.php.net/package/uploadprogress
#   - memcache - https://pecl.php.net/package/memcache
#   - gd
#       - also libpng12-dev, libjpeg62-turbo-dev, libfreetype6-dev required from apt
#   - mcrypt
#       - also libmcrypt-dev required from apt
#   - pdo_mysql, mbstring, zip and opcache
# - Download build.sh dependencies.
#
# TODO: Maybe add proper nameserver to /etc/resolv.conf? Since drush dl is giving error.
#
#
# VERSION 0.6

FROM php:5.6.11-cli
MAINTAINER Aleksi Johansson <aleksi@aleksijohansson.net>

# Put the helper script into place.
COPY provisioning/move.sh /usr/local/bin/move

# Define environment variables.
ENV USER_ID 1000

RUN \
# Add the Bro user to run Apache with permission to the files.
# Create home dir (-m) which is needed for Composer.
useradd bro -u ${USER_ID} -s /bin/bash -m \
# Update apt-get cache.
&& apt-get update \
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
&& docker-php-ext-install pdo_mysql mbstring zip opcache mcrypt memcache gd uploadprogress \
#
# Install python-yaml and git for build.sh.
&& apt-get install -y python-yaml git \
# TODO: Is this really needed? Install mysql-client for Drush.
&&  apt-get install -y mysql-client \
# Install Composer and Drush for build.sh.
&& curl -sS https://getcomposer.org/installer | php \
&& mv composer.phar /usr/local/bin/composer \
&& composer global require drush/drush:6.* \
&& su - bro -c 'composer global require drush/drush:6.*'

# Add Composer to PATH.
# Only root gets the ENV, but doesn't get the profile.d/*.sh. That's why
# the double entry.
# TODO: Check if we can use $HOME variable instead of forcing root
ENV PATH=/root/.composer/vendor/bin:$PATH
COPY provisioning/composer.sh /etc/profile.d/composer.sh
