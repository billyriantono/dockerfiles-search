FROM php:7.2-fpm

MAINTAINER Lisa Ridley <lisa@prometsource.com>

RUN apt-get update -qq \
  && apt-get install wget mysql-client unzip zip -yq \
## Packages not installed that are typically included on Acquia Cloud
## gnupg http igbinary imagick propro rapht oauth imap ldap yaml ssh2
    && apt-get update && apt-get install -y libpng-dev libjpeg-dev libpq-dev libbz2-dev libgmp-dev libmemcached-dev \
    libxml2-dev libtidy-dev libxslt-dev libyaml-dev libmcrypt-dev \
    && rm -rf /var/lib/apt/lists/* \
    && docker-php-ext-configure gd --with-png-dir=/usr --with-jpeg-dir=/usr \
    && docker-php-ext-install gd mbstring opcache pdo pdo_mysql pdo_pgsql zip mysqli bcmath bz2 calendar exif gettext gmp \
    && docker-php-ext-install pcntl shmop soap sockets \
    && docker-php-ext-install sysvmsg sysvsem sysvshm tidy wddx xmlrpc xsl \
    && pecl install memcached mcrypt-1.0.1 yaml \
    && docker-php-ext-enable memcached mcrypt yaml \
# set recommended PHP.ini settings
# see https://secure.php.net/manual/en/opcache.installation.php
    && { \
        echo 'opcache.memory_consumption=128'; \
        echo 'opcache.interned_strings_buffer=8'; \
        echo 'opcache.max_accelerated_files=4000'; \
        echo 'opcache.revalidate_freq=0'; \
        echo 'opcache.fast_shutdown=1'; \
        echo 'opcache.enable_cli=1'; \
    } > /usr/local/etc/php/conf.d/opcache-recommended.ini \
#
# Install MailHog Sendmail support.
    && apt-get update -qq && apt-get install -yq git golang-go && \
    mkdir -p /opt/go && \
    export GOPATH=/opt/go && \
    go get github.com/mailhog/mhsendmail \
    && rm -rf /var/lib/apt/lists/* \
    && apt autoremove -y \
## Install xDebug.
    && pecl install xdebug-2.7.0;

# Copy PHP configs.
COPY conf.d/* /usr/local/etc/php/conf.d/
RUN chmod 644 /usr/local/etc/php/conf.d/* \
    && curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer \
    && composer --version

WORKDIR /var/www/docroot
