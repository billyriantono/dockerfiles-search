FROM php:7.3-apache

LABEL maintainer="Slick Team <silvam.filipe@gmail.com>"

ENV USE_OPCACHE yes
ENV USE_XDEBUG no
ENV XDEBUG_VERSION 2.7.0
ENV COMPOSER_HOME /var/www/.composer
ENV PATH vendor/bin:$COMPOSER_HOME/vendor/bin:$PATH
ENV COMPOSER_VERSION 1.7.2
ENV GOSU_VERSION 1.10
ENV WEBROOT webroot

COPY bin/* /usr/local/bin/

# Install useful extensions
RUN apt-install \
      libfreetype6-dev \
      libjpeg62-turbo-dev \
      libmcrypt-dev \
      libpng-dev \
      libicu-dev \
      libmemcached-dev \
      unzip \
      zlib1g-dev libicu-dev g++ libxml2-dev \
      git rsync zlib1g-dev \
      libzip-dev

RUN docker-php-ext-install \
      mysqli \
      pdo_mysql \
      mbstring \
  && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
  && docker-php-ext-install gd \
  && docker-php-ext-configure intl && \
    docker-php-ext-install intl && \
    docker-php-ext-install opcache && \
    docker-php-ext-install soap && \
    docker-php-ext-install sockets && \
    docker-php-ext-install zip

RUN mkdir -p /usr/local/etc/php/opcache.d && \
    mv /usr/local/etc/php/conf.d/*opcache.ini /usr/local/etc/php/opcache.d/

# Install APCu
RUN pecl install apcu \
    && echo "extension=apcu.so" > /usr/local/etc/php/conf.d/apcu.ini

RUN docker-php-pecl-install xdebug-$XDEBUG_VERSION && \
    echo "xdebug.remote_enable=on\nxdebug.remote_connect_back=on" > /usr/local/etc/php/conf.d/xdebug.ini && \
    mkdir -p /usr/local/etc/php/xdebug.d && \
    mv /usr/local/etc/php/conf.d/*xdebug.ini /usr/local/etc/php/xdebug.d/

RUN apt-purge g++

# Grab gosu for easy step-down from root
RUN set -x \
  && curl -sSLo /usr/local/bin/gosu "https://github.com/tianon/gosu/releases/download/$GOSU_VERSION/gosu-$(dpkg --print-architecture)" \
  && curl -sSLo /usr/local/bin/gosu.asc "https://github.com/tianon/gosu/releases/download/$GOSU_VERSION/gosu-$(dpkg --print-architecture).asc" \
  && export GNUPGHOME="$(mktemp -d)" \
  && rm -r "$GNUPGHOME" /usr/local/bin/gosu.asc \
  && chmod +x /usr/local/bin/gosu \
  && gosu nobody true


# Include composer
RUN curl -sS https://getcomposer.org/installer | php -- \
      --install-dir=/usr/local/bin \
      --filename=composer \
      --version=${COMPOSER_VERSION}
RUN mkdir -p $COMPOSER_HOME/cache && \
    chown -R www-data:www-data /var/www && \
    echo "phar.readonly = off" > /usr/local/etc/php/conf.d/phar.ini
VOLUME $COMPOSER_HOME/cache

# Add configs
COPY etc/*.ini /usr/local/etc/php/
COPY etc/*.conf /etc/apache2/sites-available/
RUN mkdir -p /var/www/app/$WEBROOT
RUN a2enmod rewrite headers

# Add entrypoint
COPY init.d /docker-entrypoint-init.d/
COPY docker-entrypoint.sh /
ENTRYPOINT ["/docker-entrypoint.sh"]
WORKDIR /var/www/app
CMD ["apache2-foreground"]
