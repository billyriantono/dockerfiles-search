# Pull base image
FROM php:7.1-fpm

ENV PHALCON_VERSION 3.2.1
ENV COMPOSER_ALLOW_SUPERUSER 1
ENV DEBIAN_FRONTEND noninteractive

RUN cd /tmp \
    && apt-get update \
    && apt-get install -y \
        git \
        zip unzip \
        libmemcached11 \
        libmemcachedutil2 \
        libmemcached-dev \
        libz-dev \
        libssl-dev \
        libicu-dev \
        mercurial \
        gnupg \
        supervisor \
        libfreetype6-dev \
        libjpeg62-turbo-dev \
        libpng-dev \
        libmagickwand-dev \
        libtidy-dev \
    # locales
    && apt-get install -y locales \
    && sed -i '/en_US.UTF-8/s/^#//' /etc/locale.gen \
    && sed -i '/ru_RU.UTF-8/s/^#//' /etc/locale.gen \
    && locale-gen \
    # memcached
    && git clone -b php7 https://github.com/php-memcached-dev/php-memcached \
    && cd php-memcached \
    && phpize \
    && ./configure \
    && make \
    && make install \
    && cd .. \
    && rm -rf  php-memcached \
    && echo "extension=memcached.so" > /usr/local/etc/php/conf.d/memcached.ini \
    && apt-get remove -y build-essential libmemcached-dev libz-dev \
    && apt-get remove -y \
        libmemcached-dev \
        libz-dev \
    && apt-get autoremove -y \
    # mongo
    && pecl install mongodb \
    && echo "extension=mongodb.so" > /usr/local/etc/php/conf.d/mongodb.ini \
    # other extensions
    && docker-php-ext-configure intl \
    && docker-php-ext-install intl \
    && docker-php-ext-install -j$(nproc) pdo_mysql bcmath \
    && docker-php-ext-install zip \
    && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
    && docker-php-ext-install -j$(nproc) gd \
    && pecl install imagick-3.4.3 \
    && docker-php-ext-enable imagick \
    && docker-php-ext-install tidy \
    # phalcon
    && curl -sSLO https://codeload.github.com/phalcon/cphalcon/tar.gz/v$PHALCON_VERSION \
    && tar xvzf v$PHALCON_VERSION  \
    && cd cphalcon-$PHALCON_VERSION/build \
    && export CFLAGS="-O2 -g -fomit-frame-pointer" \
    && ./install \
    && echo "extension=phalcon.so" > /usr/local/etc/php/conf.d/phalcon.ini \
    # composer
    && curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer \
    && composer --version \
    # xdebug
    && pecl install xdebug \
    && docker-php-ext-enable xdebug \
    # tideways + graphviz
    && echo 'deb http://s3-eu-west-1.amazonaws.com/tideways/packages debian main' > /etc/apt/sources.list.d/tideways.list \
    && curl -sS https://s3-eu-west-1.amazonaws.com/tideways/packages/EEB5E8F4.gpg | apt-key add - \
    && apt-get update \
    && apt-get -yq install tideways-php=4.1.6 tideways-cli \
    && cp /usr/lib/tideways/tideways-php-7.1.so $(php -r 'echo ini_get("extension_dir");')/tideways.so \
    && echo "extension=tideways.so" > /usr/local/etc/php/conf.d/tideways.ini \
    && echo "tideways.auto_prepend_library=0" >> /usr/local/etc/php/conf.d/tideways.ini \
    && apt-get install -y graphviz \
    # garbage collector
    && apt-get autoremove -y \
    && apt-get autoclean -y \
    && apt-get clean -y \
    && rm -rf \
        /var/lib/apt/lists/* \
        /tmp/* \
        /var/tmp/* \
        /etc/php5 \
        /etc/php/5* \
        /usr/lib/php/20121212 \
        /usr/lib/php/20131226 \
        /var/log \
        /var/cache

ENV LANG en_US.UTF-8
ENV LANGUAGE en_US:en
ENV LC_ALL en_US.UTF-8
