FROM php:7.3-fpm-stretch
ENV XDEBUG_VERSION=2.7.1

#IMAGE DEPENDENCIES
    #CRON NEEDED TO ADD WEB CRONTABS
    #MYSQL-CLIENT NEEDED FOR MAGERUN
ENV ImageDeps="\
    cron \
    default-mysql-client \
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
        libzip-dev \
    "; \
    set -x \
    && apt-get update && apt-get install -y $ImageDeps $buildDeps --no-install-recommends \
    && rm -rf /var/lib/apt/lists/*
RUN docker-php-ext-configure gd --with-png-dir=/usr --with-jpeg-dir=/usr --with-freetype-dir=/usr \
    && docker-php-ext-install -j "$(getconf _NPROCESSORS_ONLN)" \
    gd \
    mbstring \
    mysqli \
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

# Install libsodium
RUN echo "deb http://deb.debian.org/debian stretch-backports main" >> /etc/apt/sources.list

RUN apt-get update && apt-get -t stretch-backports install -y \
  libsodium-dev

RUN pecl install -f libsodium-1.0.17

# Install SSH
RUN apt-get update && apt-get install -y openssh-server 

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

#Install sudo
RUN apt-get update && apt-get install sudo

# Add magento user, make it sudo and sudo without passwd
RUN useradd -m magento && echo "magento:magento" | chpasswd && adduser magento sudo \
    && usermod -g www-data magento
RUN echo '%sudo ALL=(ALL) NOPASSWD:ALL' >> /etc/sudoers

EXPOSE 80

CMD nginx && php-fpm
