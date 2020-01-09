FROM php:7.2-apache
RUN docker-php-ext-install mysqli pdo pdo_mysql \
    && docker-php-ext-enable mysqli pdo pdo_mysql 

 # Install needed php extensions: ldap
RUN apt-get update && apt-get install libldap2-dev -y \
    libfreetype6-dev \
    libjpeg62-turbo-dev \
    libmcrypt-dev \
    libpng-dev \
    libpng-dev \
    libmemcached-dev \
    zlib1g-dev \
    libicu-dev \
    libpq-dev \
    libssh2-1-dev \
    libxml2-dev \
    libmagickwand-dev  \
    pdftk \
    ssmtp  \
    zip \
    && rm -rf /var/lib/apt/lists/* \
        

     # configure ssmtp to read from env so php's mail() function will work out of the box. 
     && sed -ri -e 's/^(mailhub=).*/\1%%SMTP_HUB%%/' -e 's/^#(FromLineOverride)/\1/' /etc/ssmtp/ssmtp.conf

RUN docker-php-ext-configure ldap --with-libdir=lib/x86_64-linux-gnu/ \
    && docker-php-ext-install ldap \
    && docker-php-ext-install zip \
    && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
&& docker-php-ext-install -j$(nproc) gd 

RUN a2enmod authnz_ldap

RUN apt-get update && \
    apt-get install -y --no-install-recommends git

RUN curl --silent --show-error https://getcomposer.org/installer | php

RUN pecl install xdebug-2.6.0
RUN docker-php-ext-enable xdebug
RUN echo "xdebug.remote_enable=1" >> /usr/local/etc/php/php.ini
