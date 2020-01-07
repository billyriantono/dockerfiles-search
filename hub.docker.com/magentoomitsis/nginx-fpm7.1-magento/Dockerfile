FROM php:7.1-fpm
ENV XDEBUG_VERSION=2.5.0

#IMAGE DEPENDENCIES
    #CRON NEEDED TO ADD WEB CRONTABS
    #MYSQL-CLIENT NEEDED FOR MAGERUN
ENV ImageDeps="\
    cron \
    mysql-client \
    git \
"

# Install PHP7
RUN buildDeps=" \
        libpng-dev \
        libjpeg-dev \
        libmcrypt-dev \
        libxml2-dev \
        freetype* \
        libxslt1-dev \
        cron \
        libicu-dev \
        libfreetype6-dev \
    "; \
    set -x \
    && apt-get update && apt-get install -y $ImageDeps $buildDeps --no-install-recommends \
    && rm -rf /var/lib/apt/lists/*
RUN docker-php-ext-configure gd --with-png-dir=/usr --with-jpeg-dir=/usr --with-freetype-dir=/usr \
    && docker-php-ext-install -j "$(getconf _NPROCESSORS_ONLN)" \
    gd \
    mbstring \
    mysqli \
    mcrypt \
    pdo_mysql \
    soap \
    zip \
    bcmath \
    intl \
    xsl \
    && curl -s -L "http://xdebug.org/files/xdebug-${XDEBUG_VERSION}.tgz" | tar -xvz -C /tmp \
    && cd "/tmp/xdebug-${XDEBUG_VERSION}/" \
    && phpize && ./configure --enable-xdebug && make \
    && mkdir /usr/lib/php7/ && cp modules/xdebug.so /usr/lib/php7/xdebug.so \
    && touch /usr/local/etc/php/ext-xdebug.ini \
    && curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

# Configure PHP
COPY php.ini /usr/local/etc/php/php.ini
COPY php-fpm.conf /usr/local/etc/
COPY ext-xdebug.ini /usr/local/etc/php/conf.d/ext-xdebug.ini

ENV PHP_IDE_CONFIG="serverName=localhost"

# Install Nginx

RUN DEBIAN_FRONTEND=noninteractive ;\
    apt-get update && \
    apt-get install --assume-yes \
        bzip2 \
        nginx \
        libaio-dev \
        wget \
        unzip \
    && rm -rf /var/lib/apt/lists/*

RUN adduser --disabled-password --gecos "" magento \
    && usermod -g www-data magento

# Install GRUNT

RUN apt-get update && apt-get install gnupg -y \
    && curl -sL https://deb.nodesource.com/setup_8.x | bash - \
    && apt-get install -y nodejs \
    && npm install -g grunt-cli

# Install SQLSRV Extension for PHP
RUN apt-get update \
    && curl -s https://packages.microsoft.com/keys/microsoft.asc | apt-key add - \
    && curl https://packages.microsoft.com/config/debian/9/prod.list > /etc/apt/sources.list.d/mssql-release.list \
    && apt-get update -yqq \
    && ACCEPT_EULA=Y apt-get install -y msodbcsql17 unixodbc-dev unixodbc \
    && rm -r /var/lib/apt/lists/* \
    && pecl install sqlsrv pdo_sqlsrv \
    && /usr/local/bin/docker-php-ext-enable sqlsrv pdo_sqlsrv

EXPOSE 80

CMD nginx && php-fpm