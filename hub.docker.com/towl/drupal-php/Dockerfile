FROM php:7.1-fpm

LABEL maintainer="Franck Coutouly <towl.fr@gmail.com>"

#Install required library
RUN apt-get update && apt-get install -y \
        cron \
        ssmtp \
        iproute2 \
        libfreetype6-dev \
        libjpeg62-turbo-dev \
        libmcrypt-dev \
        libpng-dev \
        libedit-dev \
        libxml2-dev \
        libxslt-dev \
        libzip-dev

# Install Magento required packages
RUN docker-php-ext-install -j$(nproc) json mbstring pdo_mysql readline simplexml xml xsl xmlrpc ctype dom iconv mcrypt soap intl bcmath && \
  docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ && \
  docker-php-ext-install -j$(nproc) gd

# Install packages from pecl
RUN pecl install redis-3.1.6 \
    && pecl install xdebug-2.6.0 \
    && pecl install zip-1.15.2 \
    && docker-php-ext-enable redis xdebug zip opcache

# Install composer
RUN php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');" && \
  php -r "if (hash_file('SHA384', 'composer-setup.php') === '93b54496392c062774670ac18b134c3b3a95e5a5e5c8f1a9f115f203b75bf9a129d5daa8ba6a13e2cc8a1da0806388a8') { echo 'Installer verified'; } else { echo 'Installer corrupt'; unlink('composer-setup.php'); } echo PHP_EOL;" && \
  php composer-setup.php --install-dir=/usr/local/bin/ --filename=composer && \
  php -r "unlink('composer-setup.php');" && \
  apt install -y git unzip

# Add config
COPY conf/php.ini /usr/local/etc/php/
COPY conf/ssmtp.conf /etc/ssmtp/ssmtp.conf
COPY conf/cron /var/spool/cron/crontabs/www-data
COPY docker-entrypoint /usr/local/bin/

RUN chmod a+x /usr/local/bin/docker-entrypoint

WORKDIR /var/www/drupal

RUN useradd -u 1000 -m -s /bin/bash php && /usr/sbin/usermod -a -G www-data php && /usr/sbin/usermod -a -G php www-data

USER php

ENTRYPOINT ["docker-entrypoint"]

CMD ["php-fpm"]
