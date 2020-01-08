FROM php:7.1-apache
LABEL maintainer="kf.kawalec@gmail.com"
LABEL maintainer="bence.gazder@brixify.com"

VOLUME /root/composer

# Environmental Variables
ENV COMPOSER_HOME /root/composer

RUN apt-get update && \
    DEBIAN_FRONTEND=noninteractive apt-get install -y \
        openssh-client \
        libfreetype6-dev \
        libjpeg62-turbo-dev \
        libmcrypt-dev \
        libpng12-dev \
        libcurl4-openssl-dev \
        libldap2-dev \
        libicu-dev \
        libc-client-dev \
        libkrb5-dev \
        curl \
        libtidy* \
        git \
    && apt-get clean \
    && rm -r /var/lib/apt/lists/* && \
# PHP Extensions
    docker-php-ext-install \
        mcrypt \
        mbstring \
        curl \
        json \
        pdo_mysql \
        exif \
        tidy \
        zip \
	bcmath \
    && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
    && docker-php-ext-install gd \
    && docker-php-ext-configure ldap --with-libdir=lib/x86_64-linux-gnu \
    && docker-php-ext-install ldap \
    && docker-php-ext-configure intl \
    && docker-php-ext-install intl \
    && docker-php-ext-configure bcmath \
    && docker-php-ext-install bcmath \
    && docker-php-ext-configure imap --with-kerberos --with-imap-ssl \
    && docker-php-ext-install imap \
    && pecl install mongodb \
    && docker-php-ext-enable mongodb && \
# NodeJS
    curl -sL https://deb.nodesource.com/setup_9.x | bash - && \
    apt-get install -y nodejs && \
    apt-get clean && \
# Memory Limit
    echo "memory_limit=-1" > $PHP_INI_DIR/conf.d/memory-limit.ini && \
# Time Zone
    echo "date.timezone=Europe/Warsaw" > $PHP_INI_DIR/conf.d/date_timezone.ini && \
# Install Composer
    curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer && \
	composer selfupdate && \
# Versions
   php --version && composer --version
