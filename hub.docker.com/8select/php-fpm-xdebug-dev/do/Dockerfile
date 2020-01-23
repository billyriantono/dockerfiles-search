ARG php_version=7.1
ARG os_version=jessie
FROM php:${php_version}-fpm-${os_version}

ENV NPM_CONFIG_PREFIX=/usr/local

# patch source list for jessie
RUN echo "deb http://deb.debian.org/debian/ jessie main contrib non-free \n\
          deb-src http://deb.debian.org/debian/ jessie main contrib non-free \n\
          deb http://security.debian.org/ jessie/updates main contrib non-free \n\
          deb-src http://security.debian.org/ jessie/updates main contrib non-free" > /etc/apt/sources.list

# install extension dependencies and install dep
RUN apt-get update \
    && apt-get install -y \
         zlib1g-dev libicu-dev g++ libpng.dev libmagickwand-dev libcurl4-gnutls-dev librtmp-dev git \
         libmcrypt-dev libxml++2.6-dev libc-client-dev libkrb5-dev \
    && ln -s /usr/bin/nodejs /usr/bin/node \
    && pecl install apcu imagick \
    && docker-php-ext-enable imagick apcu \
    && docker-php-ext-configure imap --with-imap-ssl --with-kerberos \
    && docker-php-ext-configure gd --with-gd --with-jpeg-dir=/usr/include/ --with-png-dir=/usr/include/ --with-freetype-dir=/usr/include/ \
    && docker-php-ext-install intl gd curl json mbstring mcrypt opcache pdo xml zip pdo_mysql imap bcmath soap \
    && echo 'date.timezone = "Europe/Paris"' > /usr/local/etc/php/php.ini \
    && echo 'memory_limit = -1' >> /usr/local/etc/php/php.ini

# Install node8.10 and npm
RUN set -ex \
    ; apt-get update \
    ; curl -o nodejs.deb https://deb.nodesource.com/node_8.x/pool/main/n/nodejs/nodejs_8.10.0-1nodesource1_amd64.deb \
    ; dpkg -i ./nodejs.deb \
    ; rm nodejs.deb

# Install composer and set alias for easier use
RUN php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');" \
    && php composer-setup.php --install-dir=/usr/local/bin/ --filename=composer \
    && php -r "unlink('composer-setup.php');"

# Install php packages
RUN npm install -g less \
    && npm install -g --allow-root bower

# Remove useless packages
RUN apt-get autoclean -y \
    && apt-get autoremove -y \
    && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* /usr/share/doc/*

# Set start command for entrypoint
CMD ["php-fpm"]
