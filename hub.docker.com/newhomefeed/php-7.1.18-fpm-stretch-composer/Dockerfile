FROM php:7.1.18-fpm-stretch

RUN apt-get update \
    && apt-get upgrade -y \
    && apt-get install -y git
RUN pecl install mailparse && docker-php-ext-enable mailparse
RUN apt-get install -y libxslt-dev zip unzip \
    && docker-php-ext-install xsl \
    && docker-php-ext-install pcntl \
    && curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer \
    && composer -V \
    && pecl install xdebug \
    && echo "zend_extension=$(find /usr/local/lib/php/extensions/ -name xdebug.so)" > /usr/local/etc/php/conf.d/xdebug.ini

RUN curl -sL https://deb.nodesource.com/setup_8.x | bash - \
    && apt-get install -yq nodejs build-essential \
    && apt-get install -y -qq npm \ 
    && npm -v \
    && npm install --global bower \
    && bower -v \
    && npm install --global gulp \
    && gulp -v \