FROM php:7.0-fpm-stretch

ENV DEBIAN_FRONTEND=noninteractive

RUN set -ex; \
        #Install depenencies for ImageMagick \
        apt-get -y update; \
        apt-get install -y \
                libfreetype6-dev \
                libjpeg62-turbo-dev \
                libmcrypt-dev \
                libpng-dev \
                libmcrypt-dev \
                libczmq-dev \
                libicu-dev \
                libxml2 \
                libxml2-dev \
                libxslt1-dev \
                libxslt1.1 \
                libssl-dev \
                libc-client-dev \
                libkrb5-dev \
                libpspell-dev \
                ; \
        apt-get install -y \
                libmagickwand-dev --no-install-recommends \
                ; \
        apt-get clean ; \
        #Build additional PHP extensions \
        docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ ; \
        docker-php-ext-install gd; \
        pecl install imagick ; \
        pecl install zmq-beta ; \
        docker-php-ext-enable imagick ; \
        docker-php-ext-install bcmath  ; \
        docker-php-ext-enable zmq ; \
        docker-php-ext-install bcmath ; \
        docker-php-ext-install calendar ; \
        docker-php-ext-install exif ; \
        docker-php-ext-install ftp ; \
        docker-php-ext-install gettext ; \
        docker-php-ext-install hash ; \
        docker-php-ext-install iconv ; \
        docker-php-ext-configure imap --with-kerberos --with-imap-ssl ; \
        docker-php-ext-install imap ; \
        docker-php-ext-install opcache ; \
        docker-php-ext-install pspell ; \
        docker-php-ext-install mcrypt ; \
        docker-php-ext-install intl ; \
        docker-php-ext-install json ; \
        docker-php-ext-install mbstring ; \
        docker-php-ext-install mysqli ; \
        docker-php-ext-install opcache ; \
        docker-php-ext-install pcntl sockets ; \
        docker-php-ext-install pdo_mysql ; \
        docker-php-ext-install shmop ; \
        docker-php-ext-install soap ; \
        docker-php-ext-install sysvmsg ; \
        docker-php-ext-install sysvsem ; \
        docker-php-ext-install sysvshm ; \
        docker-php-ext-install wddx ; \
        docker-php-ext-install xsl ; \
        docker-php-ext-install xml ; \
        docker-php-ext-install xmlrpc ; \
        docker-php-ext-install zip ; \
        php -r "ini_set('memory_limit','250M'); readfile('http://getcomposer.org/installer');" | php -d memory_limit=250M -- --install-dir=/usr/bin/ --filename=compose

#Put our local php.ini in place
COPY php.ini /usr/local/etc/php/

