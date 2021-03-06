FROM php:fpm

MAINTAINER webfatorial <webfatorial@webfatorial.com>

COPY etc/init.d /etc/init.d
COPY usr/local/etc/php /usr/local/etc/php

RUN apt-get update
RUN apt-get -y install wget
RUN apt-get -y install libpcre3-dev
RUN apt-get -y install libmcrypt-dev
RUN apt-get -y install libfreetype6-dev
RUN apt-get -y install libjpeg62-turbo-dev
RUN apt-get -y install libjpeg-dev
RUN apt-get -y install libpng12-dev
RUN apt-get -y install locales
RUN apt-get -y install php5-common
RUN apt-get -y install php5-gd
RUN apt-get -y install php5-mcrypt
RUN apt-get -y install php5-mysql
RUN apt-get -y install pngquant
RUN apt-get -y install tzdata

RUN rm -rf /var/lib/apt/lists/*

RUN docker-php-ext-configure gd --with-png-dir=/usr --with-jpeg-dir=/usr
RUN docker-php-ext-configure opcache --enable-opcache

RUN docker-php-ext-install gd
RUN docker-php-ext-install mbstring
RUN docker-php-ext-install mcrypt
RUN docker-php-ext-install mysqli
RUN docker-php-ext-install opcache
RUN docker-php-ext-install pdo
RUN docker-php-ext-install pdo_mysql

RUN wget http://static.jonof.id.au/dl/kenutils/pngout-20130221-linux.tar.gz \
    && tar xvf pngout-20130221-linux.tar.gz \
    && mv pngout-20130221-linux/x86_64/pngout /usr/bin \
    && rm -rf pngout-20130221-linux.tar.gz

WORKDIR /var/www/html

RUN getent group www-data || groupadd www-data -g 33
RUN id -u www-data &>/dev/null || useradd -u 1000  --no-create-home --system --no-user-group www-data

RUN usermod -u 1000 www-data
RUN usermod -G staff www-data

RUN chown -R www-data:www-data /var/www/html
RUN chmod -R 775 /var/www/html

COPY config/opcache.ini $PHP_INI_DIR/conf.d/
COPY docker-entrypoint.sh /entrypoint.sh

RUN chmod +x /entrypoint.sh

VOLUME /var/www/html

ENV LOCALE en_US.UTF-8
ENV TIMEZONE America/Los_Angeles

RUN ls

ENTRYPOINT /entrypoint.sh

CMD php-fpm
