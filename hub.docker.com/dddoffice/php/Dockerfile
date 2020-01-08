FROM php:7.2.19-fpm

MAINTAINER Alexander Reiß <alexander@dasdomaindepot.de>

RUN apt-get update && apt-get install -y \
    git \
    unzip \
    zip \
    tar \
    libfreetype6-dev \
    libjpeg62-turbo-dev \
    libmcrypt-dev \
    libpng-dev \
    cron \
    rsyslog \
    libgeoip-dev \
    gnupg2 \
    && docker-php-ext-install -j$(nproc) iconv zip \
    && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/\
    && docker-php-ext-install -j$(nproc) gd

# Install intl
RUN apt-get install -y \
    zlib1g-dev\
    libicu-dev\
    g++\
    && docker-php-ext-configure intl\
    && docker-php-ext-install intl

#bcmath bz2 calendar ctype curl dba dom enchant exif fileinfo filter ftp gd gettext gmp hash iconv imap interbase intl json ldap mbstring mysqli oci8 odbc opcache pcntl pdo pdo_dblib pdo_firebird pdo_mysql pdo_oci pdo_odbc pdo_pgsql pdo_sqlite pgsql phar posix pspell readline recode reflection session shmop simplexml snmp soap sockets sodium spl standard sysvmsg sysvsem sysvshm tidy tokenizer wddx xml xmlreader xmlrpc xmlwriter xsl zend_test zip

RUN pecl channel-update pecl.php.net
RUN pecl install geoip-beta

RUN curl -sS https://getcomposer.org/installer -o composer-setup.php
RUN php composer-setup.php --install-dir=/usr/local/bin --filename=composer

# NPM installieren
RUN curl -sL https://deb.nodesource.com/setup_11.x | bash
RUN apt-get install -y nodejs
RUN npm install -g grunt

# Microsoft SQL Server Prerequisites
ENV ACCEPT_EULA=Y

RUN apt-get update \
    && curl http://packages.microsoft.com/keys/microsoft.asc | apt-key add - \
    && curl http://packages.microsoft.com/config/debian/9/prod.list \
        > /etc/apt/sources.list.d/mssql-release.list\
    && apt-get install -y --no-install-recommends \
        locales \
        apt-transport-https \
    && echo "en_US.UTF-8 UTF-8" > /etc/locale.gen \
    && locale-gen \
    && apt-get update \
    && apt-get -y --no-install-recommends install \
        unixodbc \
        unixodbc-dev \
        msodbcsql17 \
        mssql-tools

RUN docker-php-ext-install mbstring pdo pdo_mysql \
    && pecl install sqlsrv pdo_sqlsrv-5.6.0 \
    && docker-php-ext-enable sqlsrv

RUN apt-get install -y mysql-client

# install mongodb ext
RUN apt-get install -y libcurl4-openssl-dev pkg-config libssl-dev
RUN pecl install mongodb \
    && docker-php-ext-enable mongodb


# Set timezone
RUN rm /etc/localtime
RUN ln -s /usr/share/zoneinfo/Europe/Paris /etc/localtime
RUN "date"

### Update PHP Config
RUN echo 'file_uploads = On\n' \
         'memory_limit = 500M\n' \
         'upload_max_filesize = 500M\n' \
         "client_max_body_size = 500M\n" \
         "post_max_size = 500M\n" \
         "max_execution_time = 600\n" \
          'date.timezone = "Europe/Berlin"\n' \
          "date.default_latitude = 50.941357\n" \
          "date.default_longitude = 6.958307\n" \
          "extension=geoip.so\n" \
         > /usr/local/etc/php/conf.d/ddd.ini


# install xdebuga
RUN pecl install xdebug
RUN docker-php-ext-enable xdebug
RUN echo "error_reporting = E_ALL" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini
RUN echo "display_startup_errors = On" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini
RUN echo "display_errors = On" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini
RUN echo "xdebug.remote_enable=1" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini
RUN echo "xdebug.remote_connect_back=1" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini
RUN echo "xdebug.idekey=\"PHPSTORM\"" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini
RUN echo "xdebug.remote_port=9000" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini
RUN echo "xdebug.max_nesting_level = 5000" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini


RUN echo 'alias sf="php app/console"' >> ~/.bashrc
RUN echo 'alias sf3="php bin/console"' >> ~/.bashrc

WORKDIR /usr/share/nginx/html/