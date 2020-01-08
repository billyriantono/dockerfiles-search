FROM debian:jessie
MAINTAINER https://github.com/atolcd/docker-magento-php-apache

# persistent / runtime deps
RUN apt-get update && apt-get install -y --no-install-recommends \
      ca-certificates \
      curl \
      librecode0 \
      libmysqlclient-dev \
      libsqlite3-0 \
      libxml2 \
      file \
      autoconf \
      g++ \
      gcc \
      libc-dev \
      make \
      pkg-config \
      re2c \
      apache2-bin \
      apache2-dev \
      apache2.2-common \
      mcrypt \
      libmcrypt-dev \
      && apt-get clean \
      && rm -r /var/lib/apt/lists/*

##<apache2>##
RUN rm -rf /var/www/html && mkdir -p /var/lock/apache2 /var/run/apache2 /var/log/apache2 /var/www/html && chown -R www-data:www-data /var/lock/apache2 /var/run/apache2 /var/log/apache2 /var/www/html

# Apache + PHP requires preforking Apache for best results
RUN a2dismod mpm_event && a2enmod mpm_prefork

RUN mv /etc/apache2/apache2.conf /etc/apache2/apache2.conf.dist
COPY apache2.conf /etc/apache2/apache2.conf
##</apache2>##

# compile openssl, otherwise --with-openssl won't work
RUN CFLAGS="-fPIC" && OPENSSL_VERSION="1.0.2d" \
      && cd /tmp \
      && mkdir openssl \
      && echo "671c36487785628a703374c652ad2cebea45fa920ae5681515df25d9f2c9a8c8 openssl.tar.gz" > openssl.tar.gz.sha \
      && curl -sL "https://www.openssl.org/source/openssl-$OPENSSL_VERSION.tar.gz" -o openssl.tar.gz \
      && sha256sum -c openssl.tar.gz.sha \
      && tar -xzf openssl.tar.gz -C openssl --strip-components=1 \
      && cd /tmp/openssl \
      && ./config -fPIC && make && make install \
      && rm -rf /tmp/*

ENV PHP_INI_DIR /etc/php5/apache2
ENV PHP_VERSION 5.5.9
RUN mkdir -p $PHP_INI_DIR/conf.d

# php 5.3 needs older autoconf
# --enable-mysqlnd is included below because it's harder to compile after the fact the extensions are (since it's a plugin for several extensions, not an extension in itself)
RUN buildDeps=" \
      apache2-dev \
      autoconf2.13 \
      libcurl4-openssl-dev \
      libreadline6-dev \
      librecode-dev \
      libsqlite3-dev \
      libssl-dev \
      libxml2-dev \
      libpng-dev \
      xz-utils \
      autoconf \
      g++ \
      gcc \
      libc-dev \
      make \
      pkg-config \
      re2c \
      " \
      && set -x \
      && apt-get update && apt-get install -y $buildDeps --no-install-recommends && rm -rf /var/lib/apt/lists/* \
      && echo "ec1bf0cb3be80240049dbd92c272d4bf242a614fa5f9dcc42a15adb5fd01ccde php.tar.gz" > php.tar.gz.sha \
      && curl -SL "http://php.net/get/php-$PHP_VERSION.tar.gz/from/this/mirror" -o php.tar.gz \
      && sha256sum -c php.tar.gz.sha \
      && mkdir -p /usr/src/php \
      && tar -xof php.tar.gz -C /usr/src/php --strip-components=1 \
      && rm php.tar.gz* \
      && cd /usr/src/php \
      && ./configure --disable-cgi \
      $(command -v apxs2 > /dev/null 2>&1 && echo '--with-apxs2=/usr/bin/apxs2' || true) \
      --with-config-file-path="$PHP_INI_DIR" \
      --with-config-file-scan-dir="$PHP_INI_DIR/conf.d" \
      --enable-ftp \
      --enable-mbstring \
      --enable-mysqlnd \
      --with-mysql \
      --with-mysqli \
      --with-pdo-mysql \
      --with-curl \
      --with-mcrypt=/usr/lib/libmcrypt.so \
      --with-openssl=/usr/local/ssl \
      --enable-soap \
      --with-png \
      --with-gd \
      --with-readline \
      --with-recode \
      --with-zlib \
      && make -j"$(nproc)" \
      && make install \
      && pecl install xdebug-2.2.7 \
      && { find /usr/local/bin /usr/local/sbin -type f -executable -exec strip --strip-all '{}' + || true; } \
      && make clean \
      && apt-get purge -y --auto-remove -o APT::AutoRemove::RecommendsImportant=false -o APT::AutoRemove::SuggestsImportant=false $buildDeps 

RUN echo "default_charset = UTF-8" > $PHP_INI_DIR/php.ini \
      && echo "date.timezone = Europe/Paris" >> $PHP_INI_DIR/php.ini \
      && echo "zend_extension=/usr/local/lib/php/extensions/no-debug-non-zts-20100525/xdebug.so" >> $PHP_INI_DIR/conf.d/docker-php-ext-xdebug.ini \
      && echo "xdebug.remote_enable=1" >> $PHP_INI_DIR/conf.d/docker-php-ext-xdebug.ini \
      && echo "xdebug.remote_port=9000" >> $PHP_INI_DIR/conf.d/docker-php-ext-xdebug.ini \
      && echo "xdebug.remote_connect_back=1" >> $PHP_INI_DIR/conf.d/docker-php-ext-xdebug.ini

COPY docker-php-* /usr/local/bin/
COPY apache2-foreground /usr/local/bin/

WORKDIR /var/www/html

EXPOSE 80
CMD ["apache2-foreground"]
