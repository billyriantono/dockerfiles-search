FROM php:5.6-apache

RUN a2enmod rewrite

RUN apt-get update && apt-get install -y pv git zlib1g-dev ssmtp libpng-dev mariadb-client libxml2-dev libpng-dev libjpeg62-turbo-dev libfreetype6-dev && rm -rf /var/lib/apt/lists/*

RUN pecl install -o -f redis-2.2.8 && rm -rf /tmp/pear && echo "extension=redis.so" > /usr/local/etc/php/conf.d/redis.ini

RUN docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/
RUN docker-php-ext-install zip pdo_mysql mysql gd soap mysqli

RUN pecl install xdebug-2.5.5 && echo "zend_extension=$(find /usr/local/lib/php/extensions/ -name xdebug.so)" > /usr/local/etc/php/conf.d/xdebug.ini \
    && echo "xdebug.remote_enable=on" >> /usr/local/etc/php/conf.d/xdebug.ini \
    && echo "xdebug.remote_autostart=off" >> /usr/local/etc/php/conf.d/xdebug.ini \
    && rm -rf /tmp/pear

RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer
#RUN echo "FromLineOverride=YES\nmailhub=smtp\n" > /etc/ssmtp/ssmtp.conf
#COPY ssmtp.conf /usr/local/etc/php/conf.d/mail.ini

ARG wwwdatauid=1000
RUN usermod -u $wwwdatauid www-data
