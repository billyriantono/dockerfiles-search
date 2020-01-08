FROM php:7.1-fpm

LABEL maintainer="Franck Coutouly <towl.fr@gmail.com>"

#Install required library
RUN apt-get update && apt-get install -y \
        cron \
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
    && docker-php-ext-enable redis xdebug zip

# Install composer
RUN php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');" && \
  php composer-setup.php --install-dir=/usr/local/bin/ --filename=composer && \
  php -r "unlink('composer-setup.php');"

# Add config
COPY conf/php.ini /usr/local/etc/php/
COPY conf/zz-docker.conf /usr/local/etc/php-fpm.d/
COPY docker-entrypoint /usr/local/bin/

RUN chmod a+x /usr/local/bin/docker-entrypoint

RUN useradd -u 1000 -g www-data -m php

WORKDIR /var/www

ENTRYPOINT ["docker-entrypoint"]

CMD ["php-fpm"]
