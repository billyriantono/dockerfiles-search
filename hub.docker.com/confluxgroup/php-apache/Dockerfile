# Dockerfile
FROM phusion/baseimage:0.11
ENV DEBIAN_FRONTEND noninteractive

ENV PHP_VERSION 7.0
ENV PHP_INI_PATH /etc/php/7.0

# Install PHP
RUN add-apt-repository -y ppa:ondrej/php \
    && apt-get update \
    && apt-get install -y \
        nano \
        git \
        unzip \
        # Only install the php extensions you need.
        php$PHP_VERSION \
        php$PHP_VERSION-imagick \
        php$PHP_VERSION-intl \
        php$PHP_VERSION-mbstring \
        php$PHP_VERSION-xml \
        php$PHP_VERSION-dom \
        php$PHP_VERSION-zip \
        php$PHP_VERSION-curl \
        php$PHP_VERSION-gmp \
        php$PHP_VERSION-mysql \
        php$PHP_VERSION-curl \
        php$PHP_VERSION-gd \
        php$PHP_VERSION-imap \
        php$PHP_VERSION-tidy \
        php$PHP_VERSION-iconv \
        php$PHP_VERSION-mcrypt \
        apache2 \
        libapache2-mod-php$PHP_VERSION \
    && rm -rf /var/lib/apt/lists/*

COPY ./10-change-uid-gid.sh /etc/my_init.d/
RUN chmod +x /etc/my_init.d/10-change-uid-gid.sh

# configure apache
RUN a2enmod rewrite include expires deflate headers
COPY ./site.conf /etc/apache2/sites-available/000-default.conf

# forward apache request and error logs to docker log collector
RUN ln -sf /dev/stdout /var/log/apache2/access.log
RUN ln -sf /dev/stderr /var/log/apache2/error.log

# set a default timezone in php
RUN sed -i "s/;date.timezone =.*/date.timezone = UTC/" $PHP_INI_PATH/apache2/php.ini
RUN sed -i "s/;date.timezone =.*/date.timezone = UTC/" $PHP_INI_PATH/cli/php.ini

# enable "zlib.output_compression" in php.ini
# see http://stackoverflow.com/questions/14039804/error-330-neterr-content-decoding-failed
RUN sed -i "s/zlib\.output_compression =.*/zlib.output_compression = On/" $PHP_INI_PATH/apache2/php.ini
RUN sed -i "s/zlib\.output_compression =.*/zlib.output_compression = On/" $PHP_INI_PATH/cli/php.ini

# conigure apache to run as "vector" user
RUN sed -i "s/APACHE_RUN_USER=.*/APACHE_RUN_USER=www-data/" /etc/apache2/envvars
RUN sed -i "s/APACHE_RUN_GROUP=.*/APACHE_RUN_GROUP=www-data/" /etc/apache2/envvars

# configure services to run in this container
RUN mkdir       /etc/service/apache
ADD ./apache.sh  /etc/service/apache/run
RUN chmod +x    /etc/service/apache/run



# install composer
WORKDIR /tmp
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/bin/ --filename=composer

WORKDIR /var/www/
CMD ["/sbin/my_init"]