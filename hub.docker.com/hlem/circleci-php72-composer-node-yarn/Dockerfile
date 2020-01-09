FROM php:7.2.5

RUN set -x \
 && apt-get update -y \
 && apt-get install -y wget gnupg apt-transport-https \
 && curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | apt-key add - \
 && echo "deb https://dl.yarnpkg.com/debian/ stable main" | tee /etc/apt/sources.list.d/yarn.list \
 && curl -sL https://deb.nodesource.com/setup_12.x | bash - \
 && apt-get update -y \
 && apt-get install -y git zip libcurl4-gnutls-dev libicu-dev \
                       libfreetype6-dev libjpeg-dev libpng-dev libxml2-dev \
                       libbz2-dev libc-client-dev libkrb5-dev  mysql-client \
                       nodejs yarn \
 && docker-php-ext-install mbstring curl json intl gd xml zip bz2 opcache pdo_mysql pcntl exif bcmath \
 && echo "date.timezone = Europe/Berlin" > /usr/local/etc/php/conf.d/timezone.ini \
 && echo "memory_limit = -1" > /usr/local/etc/php/conf.d/memory.ini  \
 && wget -O /usr/local/bin/composer https://getcomposer.org/download/1.6.3/composer.phar \
 && chmod +x /usr/local/bin/composer \
 && apt-get autoclean -y \
 && apt-get --purge autoremove -y \
 && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* \
 && php -i \
 && yarn --version \
 && node --version
