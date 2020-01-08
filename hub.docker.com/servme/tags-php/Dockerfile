FROM php:7.2.4-fpm

WORKDIR /var/www/tags

RUN apt-get update && \
    apt-get install -y libmcrypt-dev libpq-dev cron zlib1g-dev libfcgi0ldbl libpng-dev git zip wget gnupg && \
    rm -rf /var/lib/apt/lists/*

RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

RUN docker-php-ext-install bcmath mbstring opcache pdo_mysql

ADD . /var/www/tags
RUN composer install && composer dumpautoload

RUN echo 'deb http://apt.newrelic.com/debian/ newrelic non-free' | tee /etc/apt/sources.list.d/newrelic.list && \
    wget -O- https://download.newrelic.com/548C16BF.gpg | apt-key add - && \
    apt-get update && \
    apt-get install -y newrelic-php5 && \
    NR_INSTALL_SILENT=1 newrelic-install install NR_INSTALL_KEY=d67b96fe940cfaea0100adc5275dd8616213b9ec

COPY docker/newrelic.ini  /usr/local/etc/php/conf.d/newrelic.ini
