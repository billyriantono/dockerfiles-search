FROM amd64/php:7.1-cli-stretch

LABEL maintainer  "Jens Dutzi <jens.dutzi@tf-network.de>"

# define working-directory.
ENV WORKDIR /home/workspace
WORKDIR ${WORKDIR}

#
# installing needed extra-libs etc.
#

RUN apt-get update && \
    DEBIAN_FRONTEND=noninteractive apt-get install -o APT::Install-Suggests=0 -o APT::Install-Recommends=0 -y \
        apt-transport-https \
        lsb-release \
        gnupg \
        libfreetype6-dev \
        libjpeg62-turbo-dev \
        libmcrypt-dev \
        libpng-dev \
        libcurl4-openssl-dev \
        libicu-dev \
        libc-client-dev \
		libkrb5-dev \
        libxml2-dev \
		ssh \
        curl \
        git \
        wget \
        unzip \
        libbz2-dev

#
# Installation of NodeJS
#

# adding NodeJS-Repository and install NodeJS
RUN curl -s https://deb.nodesource.com/gpgkey/nodesource.gpg.key | apt-key add -
RUN echo 'deb https://deb.nodesource.com/node_10.x stretch main' > /etc/apt/sources.list.d/nodesource.list
RUN echo 'deb-src https://deb.nodesource.com/node_10.x stretch main' >> /etc/apt/sources.list.d/nodesource.list

RUN apt-get update \
    && DEBIAN_FRONTEND=noninteractive apt-get install -o APT::Install-Suggests=0 -o APT::Install-Recommends=0 -y nodejs

#
# Configuration of PHP and adding some PHP Modules and Xdebug
#

# PHP Install xdebug
RUN pecl install xdebug && \
        docker-php-ext-enable xdebug

RUN docker-php-ext-install \
        pdo_mysql \
        mysqli \
        exif \
        bz2 \
        opcache \
        calendar \
        shmop \
    && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
    && docker-php-ext-install gd \
    && docker-php-ext-configure intl \
    && docker-php-ext-install intl \
    && docker-php-ext-configure imap --with-kerberos --with-imap-ssl \
    && docker-php-ext-install imap

# Memory Limit und Timezone PHP Setting
RUN echo "memory_limit=-1" > $PHP_INI_DIR/conf.d/memory-limit.ini
RUN echo "date.timezone=Europe/Berlin" > $PHP_INI_DIR/conf.d/date_timezone.ini

#
# Installation: composer
#

#Composer Volume anlegen
VOLUME /root/composer

# Environmental Variables
ENV COMPOSER_HOME /root/composer

# Install composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer && \
    composer selfupdate

# Run composer -components and phpunit installation.
RUN composer require "phpunit/phpunit=*" --prefer-source --no-interaction && \
    ln -s /home/workspace/vendor/bin/phpunit /usr/local/bin/phpunit
RUN composer require "squizlabs/php_codesniffer=*" --prefer-source --no-interaction && \
    ln -s /home/workspace/vendor/bin/phpcs /usr/local/bin/phpcs
RUN composer require "phpmd/phpmd=*" --prefer-source --no-interaction && \
    ln -s /home/workspace/vendor/bin/phpmd /usr/local/bin/phpmd
RUN composer require "sebastian/phpcpd=*" --prefer-source --no-interaction && \
    ln -s /home/workspace/vendor/bin/phpcpd /usr/local/bin/phpcpd

# Run composer and wapmorgan/php-code-fixer installation.
RUN composer require "wapmorgan/php-code-fixer=*" --prefer-source --no-interaction && \
    ln -s /home/workspace/vendor/bin/phpcf /usr/local/bin/phpcf

#
# Installation: bowser / gulp
#

# Allow root for bower
RUN echo '{ "allow_root": true }' > /root/.bowerrc

# Run installation of bower and gulp
RUN npm install -g gulp bower

# Image cleanup
RUN apt-get -yqq autoremove && \
    apt-get -yqq clean && \
    rm -rf /var/lib/apt/lists/* /var/cache/* /tmp/* /var/tmp/*

#
# Clean Up Image
#

RUN apt-get clean && rm -r /var/lib/apt/lists/*

#
# Debug: Display Version-Infos
#

RUN node --version
RUN bower -v
RUN gulp -v
RUN php --version
RUN composer --version
RUN phpunit --version
RUN phpcs --version
RUN phpcpd --version
RUN phpcf --version
