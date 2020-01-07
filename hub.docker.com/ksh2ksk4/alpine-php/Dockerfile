FROM alpine:latest
MAINTAINER ksh2ksk4 <ksh2ksk4+docker.com@gmail.com>

ENV TIMEZONE='Asia/Tokyo' \
    DISTRIBUTIONS="./distributions"

RUN apk update && \
    apk upgrade && \
    # Change the timezone
    apk add tzdata && \
    cp /usr/share/zoneinfo/${TIMEZONE} /etc/localtime && \
    echo "${TIMEZONE}" >/etc/timezone && \
    # Install some packages
    apk add --virtual _postfix-packages_ postfix && \
    apk add --virtual _nginx-packages_ nginx && \
    apk add --virtual _php-packages_ \
        php7 \
#        php7-apache2 \
#        php7-apcu \
        php7-bcmath \
#        php7-bz2 \
#        php7-calendar \
#        php7-cgi \
#        php7-common \
        php7-ctype \
        php7-curl \
#        php7-dba \
#        php7-dev \
#        php7-doc \
        php7-dom \
#        php7-embed \
#        php7-enchant \
#        php7-exif \
        php7-fpm \
        php7-ftp \
        php7-gd \
#        php7-gettext \
        php7-gmp \
#        php7-iconv \
#        php7-imap \
        php7-intl \
        php7-json \
#        php7-ldap \
#        php7-litespeed \
        php7-mbstring \
        php7-mcrypt \
#        php7-mysqli \
        php7-mysqlnd \
#        php7-odbc \
#        php7-opcache \
#        php7-openssl \
#        php7-pcntl \
        php7-pdo \
#        php7-pdo_dblib \
        php7-pdo_mysql \
#        php7-pdo_odbc \
#        php7-pdo_pgsql \
#        php7-pdo_sqlite \
        php7-pear \
#        php7-pgsql \
#        php7-phar \
#        php7-phpdbg \
#        php7-posix \
#        php7-pspell \
#        php7-session \
#        php7-shmop \
#        php7-snmp \
        php7-soap \
#        php7-sockets \
#        php7-sqlite3 \
#        php7-sysvmsg \
#        php7-sysvsem \
#        php7-sysvshm \
#        php7-tidy \
#        php7-wddx \
        php7-xdebug \
        php7-xml \
#        php7-xmlreader \
#        php7-xmlrpc \
#        php7-xsl \
        php7-zip \
        php7-zlib && \
    apk add --virtual _gnupg-packages_ \
        gnupg \
        gpgme && \
    apk add --virtual _build-packages_ \
        alpine-sdk \
        autoconf \
        php7-dev \
        gpgme-dev && \
    apk add --virtual _base-packages_ \
        bash \
        file \
        findutils \
        less && \
    # Install some extension by the PECL
    sed -i -e '/^exec/s/ -n / /' $(which pecl) && \
    pecl install gnupg && \
    echo 'extension=gnupg.so' >/etc/php7/conf.d/gnupg.ini && \
    # Uninstall some unnecessary packages
    apk del --purge _build-packages_ && \
    # Some settings
    mkdir -p /run/nginx /run/php-fpm /var/log/nginx /usr/local/share/fuelphp && \
    echo '<?php phpinfo();' >/var/lib/nginx/html/i.php

COPY ${DISTRIBUTIONS}/root/* /root/
COPY ${DISTRIBUTIONS}/nginx/nginx.conf /etc/nginx/
COPY ${DISTRIBUTIONS}/nginx/conf.d/* /etc/nginx/conf.d/
COPY ${DISTRIBUTIONS}/php/php.ini /etc/php7/
COPY ${DISTRIBUTIONS}/php/php-fpm.conf /etc/php7/
COPY ${DISTRIBUTIONS}/php/php-fpm.d/* /etc/php7/php-fpm.d/

EXPOSE 80 443

ENTRYPOINT ["/root/entrypoint.sh"]
