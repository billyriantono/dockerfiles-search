FROM php:7.0-apache
RUN apt-get update

RUN apt-get install -y libbz2-dev && docker-php-ext-install bz2

RUN apt-get install -y libcurl4-openssl-dev && docker-php-ext-install curl

RUN apt-get install -y libfreetype6-dev libgd-dev && \
    docker-php-ext-configure gd --with-freetype-dir=/usr && \
    docker-php-ext-install gd exif

RUN apt-get install -y libxslt1-dev && docker-php-ext-install xsl

RUN apt-get install -y libmcrypt-dev && docker-php-ext-install mcrypt

RUN apt-get install -y libgettextpo-dev && docker-php-ext-install gettext

RUN apt-get install -y libgmp-dev && \
    ln -s /usr/include/x86_64-linux-gnu/gmp.h /usr/local/include/ && \
    docker-php-ext-install gmp

RUN apt-get install -y libc-client-dev libkrb5-dev && \
    docker-php-ext-configure imap --with-kerberos --with-imap-ssl && \
    docker-php-ext-install imap

RUN docker-php-ext-install bcmath \
dba \
mysqli \
opcache \
pcntl \
pdo_mysql \
soap \
sockets \
sysvmsg \
sysvsem \
sysvshm \
wddx

RUN apt-get install -y libldap2-dev && \
        docker-php-ext-configure ldap --with-libdir=/lib/x86_64-linux-gnu && \
        docker-php-ext-install ldap

RUN apt-get install -y librecode-dev && docker-php-ext-install recode

RUN apt-get install -y libtidy-dev && docker-php-ext-install tidy

RUN apt-get install -y libsnmp-dev && docker-php-ext-install snmp

RUN apt-get install -y libpspell-dev && docker-php-ext-install pspell

RUN apt-get install -y libenchant-dev && docker-php-ext-install enchant

RUN apt-get install -y zlib1g-dev && docker-php-ext-install zip

RUN apt-get install -y libpq-dev && docker-php-ext-install pdo_pgsql pgsql

RUN a2enmod rewrite

RUN apt-get autoremove -y && apt-get clean all

RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/bin --filename=composer

COPY php.ini /usr/local/etc/php/

CMD apache2-foreground
