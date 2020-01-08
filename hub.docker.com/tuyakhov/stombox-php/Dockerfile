#########################################################################
#
# A Stombox PHP-FPM container - used by our API
#
# Build with:
#  docker build -t="tuyakhov/stombox-php" .
#
#
########################################################################

# Base from official php-fpm image
FROM php:5.6-fpm

RUN apt-get update && apt-get install -y \
        libmcrypt-dev \
        libssl-dev \
        libsasl2-dev \
        zlib1g-dev \
    && docker-php-ext-install mcrypt \
    && docker-php-ext-install mbstring \
    && docker-php-ext-install zip

# Waiting for mongodb-1.1
RUN pecl install -o -f mongodb \
    &&  rm -rf /tmp/pear \
    &&  echo "extension=mongodb.so" > /usr/local/etc/php/conf.d/mongodb.ini