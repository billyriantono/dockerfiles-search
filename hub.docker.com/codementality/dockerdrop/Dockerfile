FROM php:7.1-fpm

MAINTAINER Lisa Ridley "lhridley@gmail.com"

# Install packages for PHP
RUN apt-get update && apt-get install -y \
        git \
        tar \
        wget \
        ## for GD Image extension (3)
        libfreetype6-dev \
        libjpeg62-turbo-dev \
        libpng12-dev \
        ## for Mcrypt extension
        libmcrypt-dev \
        ## for extensions dependent on xml2 library headers
        libxml2-dev \
        ## for extensions dependent on ssl library headers
        libssl-dev \
        ## for extensions needing libc support
        libc-client-dev \
        ## for bz2
        libbz2-dev \
        ## for imap with kerberos support
        libkrb5-dev \
        ## for ldap (2)
        libldb-dev \
        libldap2-dev \
        ## for intl
        libicu-dev \
        ## for zip extension (2)
        unzip \
        zip \
        ## for ODBC extensions
        unixODBC-dev \
        ## for Mariadb
        mariadb-client \
        ## for Postgres (2)
        postgresql-client-9.4 \
        libpq-dev \
        ## Pear/PECL and php-dev header support
        php-pear \
        php5-dev \
    ## symlink Ldap libraries to /usr/lib so configure can find them (2 lines)
    && ln -s /usr/lib/x86_64-linux-gnu/libldap.so /usr/lib/libldap.so \
    && ln -s /usr/lib/x86_64-linux-gnu/liblber.so /usr/lib/liblber.so \
    ## Iconv and mcrypt extension
    && docker-php-ext-install -j$(nproc) iconv mcrypt \
    ## GD Image Library support
    && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
    && docker-php-ext-install -j$(nproc) gd \
    ## Mysql library support (2)
    && docker-php-ext-install pdo_mysql \
    && docker-php-ext-install mysqli \
    ## Zip extension
    && docker-php-ext-install zip \
    ## Opcaching extension
    && docker-php-ext-install opcache \
    ## Postgres extensions (3)
    && docker-php-ext-install pgsql \
    && docker-php-ext-configure pgsql -with-pgsql=/usr/local/pgsql \
    && docker-php-ext-install -j$(nproc) pdo_pgsql \
    ## Sockets support
    && docker-php-ext-install sockets \
    ## bcmath support
    && docker-php-ext-install bcmath \
    ## bz2 support
    && docker-php-ext-install bz2 \
    ## intl extension
    && docker-php-ext-install intl \
    ## pcntl extension
    && docker-php-ext-install pcntl \
    ## calendar extension
    && docker-php-ext-install calendar \
    ## imap extension
    && docker-php-ext-configure imap --with-kerberos --with-imap-ssl \
    ## ldap extension
    && docker-php-ext-install ldap \
    ## soap / wddx extensions (xml already installed)
    && docker-php-ext-install soap \
    && docker-php-ext-install wddx

#install memcached
RUN apt-get install -y \
        libmemcached11 \
        libmemcachedutil2 \
        libmemcached-dev \
        libz-dev \
    && cd /root \
    && git clone -b php7 https://github.com/php-memcached-dev/php-memcached \
    && cd php-memcached \
    && phpize \
    && ./configure \
    && make \
    && make install \
    && cd .. \
    && rm -rf  php-memcached \
    && echo extension=memcached.so >> /usr/local/etc/php/conf.d/memcached.ini \
    && apt-get remove -y build-essential libmemcached-dev libz-dev

#install redis php extension from source
RUN git clone -b php7 https://github.com/phpredis/phpredis.git \
    && cd phpredis \
    && phpize \
    && ./configure \
    && make \
    && make install \
    && cd .. \
    && rm -Rf phpredis \
    && echo extension=redis.so >> /usr/local/etc/php/conf.d/redis.ini

#install xdebug
RUN mkdir -p ~/downloads \
    && wget -O ~/downloads/xdebug-2.4.0.tgz http://xdebug.org/files/xdebug-2.4.0.tgz \
    && cd ~/downloads \
    && tar -xvzf xdebug-2.4.0.tgz \
    && cd xdebug-2.4.0 \
    && phpize \
    && ./configure \
    && make \
    && make install \
    && cd .. \
    && rm -Rf xdebug-2.4.0
COPY ./ini/xdebug.ini /usr/local/etc/php/conf.d/xdebug.ini

#install composer
RUN php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');" \
    && php -r "if (hash_file('SHA384', 'composer-setup.php') === 'c32408bcd017c577ce80605420e5987ce947a5609e8443dd72cd3867cc3a0cf442e5bf4edddbcbe72246a953a6c48e21') { echo 'Installer verified'; } else { echo 'Installer corrupt'; unlink('composer-setup.php'); } echo PHP_EOL;" \
    && php composer-setup.php \
    && php -r "unlink('composer-setup.php');" \
    && mv composer.phar /usr/local/bin/composer \
    && apt-get update && apt-get install -y \
        ca-certificates

#install drush
RUN php -r "readfile('https://s3.amazonaws.com/files.drush.org/drush.phar');" > drush \
    && chmod +x drush \
    && mv drush /usr/local/bin \
    && drush init -y

## Uninstalls ca-certificates and wget, removes unnecessary packages remnants
RUN apt-get purge -y --auto-remove wget \
    && apt-get autoremove -y \
    && rm -rf /var/lib/apt/lists/* \
    && apt-get clean

#moves all .ini files to /usr/local/etc/php/conf-available
RUN cp -r /usr/local/etc/php/conf.d /usr/local/etc/php/conf-available

#copies the php.ini template file to conf.d
COPY ini/php.ini /usr/local/etc/php/conf.d

COPY docker-entrypoint.sh /usr/local/bin/

# Changes ownershiw of /usr/local/etc to www-data:www-data
RUN chown -Rf www-data:www-data /usr/local/etc
RUN chown -Rf www-data:www-data /usr/local/bin/docker-entrypoint.sh
RUN chown -Rf www-data:www-data /var/www

# Sets container user as www-data
USER www-data

ENTRYPOINT ["docker-entrypoint.sh"]

CMD ["php-fpm"]
