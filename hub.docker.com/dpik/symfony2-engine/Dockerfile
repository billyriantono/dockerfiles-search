FROM node:9.3 as node

FROM php:5.6-apache
MAINTAINER Damien PIQUET <dpiquet@teicee.com>

# Copy nodejs from node image
COPY --from=node /usr/local/bin/node /usr/local/bin/node
COPY --from=node /opt/yarn /opt/yarn
COPY --from=node /usr/local/lib/node_modules /usr/local/lib/node_modules
COPY --from=node /usr/local/bin /usr/local/bin

# Custom Vhost
ADD 000-default.conf /etc/apache2/sites-available/000-default.conf

RUN set -xe \
    # Install PHP dependencies
    && apt-get update && apt-get install -y git subversion openssh-client coreutils unzip postgresql-client \
    && apt-get install -y autoconf gcc g++ libpq-dev binutils-gold libgcc1 linux-headers-amd64 make python libmcrypt-dev libpng-dev libjpeg-dev libc-dev libfreetype6-dev libmcrypt-dev libicu-dev \
    && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \

    # Install Xdebug
    && pecl install xdebug \
    && echo 'zend_extension=/usr/local/lib/php/extensions/no-debug-non-zts-20131226/xdebug.so' > /usr/local/etc/php/conf.d/xdebug.ini \

    # Configuration PHP
    && docker-php-ext-install -j$(nproc) iconv mbstring mcrypt intl pdo_pgsql gd zip bcmath \
    && docker-php-source delete \
    && echo "Installing composer" \

    # Install composer
    && php -r "readfile('https://getcomposer.org/installer');" | php -- --install-dir=/usr/local/bin --filename=composer \
    && chmod +x /usr/local/bin/composer \

    # Install nodejs packages
    && npm install -g less \
    && npm install -g uglify-js \
    && npm install -g uglifycss \

    # Enable httpd mod_rewrite
    && a2enmod rewrite \

    # Suppression des dépendances de build
    && apt-get remove -y autoconf gcc g++ libpq-dev linux-headers-amd64 make libmcrypt-dev libicu-dev \
    && apt-get clean

EXPOSE 80
