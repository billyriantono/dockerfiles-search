FROM php:7.0-fpm

MAINTAINER Pawel Zareba <zareba.pawel@gmail.com>

ENV REFRESHED_AT 2016-11-29 00:07

RUN apt-get update \
    && apt-get install -y \
    git \
    curl \
    unzip \
    vim \
    libzmq-dev

RUN pecl install zmq-beta

RUN docker-php-ext-enable zmq

# Memory Limit
RUN echo "memory_limit=-1" > $PHP_INI_DIR/conf.d/memory-limit.ini

# Time Zone
RUN echo "date.timezone=${PHP_TIMEZONE:-UTC}" > $PHP_INI_DIR/conf.d/date_timezone.ini

# Setup the Composer
RUN curl -o /tmp/composer-setup.php https://getcomposer.org/installer \
  && curl -o /tmp/composer-setup.sig https://composer.github.io/installer.sig \
  && php -r "if (hash('SHA384', file_get_contents('/tmp/composer-setup.php')) !== trim(file_get_contents('/tmp/composer-setup.sig'))) { unlink('/tmp/composer-setup.php'); echo 'Invalid installer' . PHP_EOL; exit(1); }" \
  && cd /tmp \
  && php /tmp/composer-setup.php \
  && mv /tmp/composer.phar /usr/local/bin/composer \
  && rm -rf /tmp/*