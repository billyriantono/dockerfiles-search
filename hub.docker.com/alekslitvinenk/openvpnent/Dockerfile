FROM php:7.2-fpm-alpine3.7
RUN set -ex \
        && apk update \
    && apk add --no-cache git curl openssh-client icu libpng freetype libjpeg-turbo postgresql-dev libffi-dev libmemcached-dev libcurl libintl gettext-dev \
    && apk add --no-cache --virtual build-dependencies icu-dev libxml2-dev freetype-dev libpng-dev libjpeg-turbo-dev g++ make autoconf \
    && apk add --no-cache php7-pear \
    && pecl install apcu \
    && pecl install apcu_bc \
    && echo 'extension = apcu.so' > /usr/local/etc/php/conf.d/apcu_bc.ini \
    && echo 'extension = apc.so' >> /usr/local/etc/php/conf.d/apcu_bc.ini \
    && pecl install igbinary \
    && pecl install memcached \
    && apk add libcurl \
    && apk add curl-dev \
    && wget -O "pecl-search_engine-solr-master.tar.gz" https://github.com/php/pecl-search_engine-solr/archive/master.tar.gz \
    && tar -zxvf pecl-search_engine-solr-master.tar.gz \
    && cd pecl-search_engine-solr-master \
    && phpize \
    && ./configure \
    && make install \
    && cd .. \
    && rm -rf pecl-search_engine-solr-master.tar.gz pecl-search_engine-solr-master \
    && apk add rabbitmq-c-dev \
    && pecl install amqp \
    && wget -O "pinba_extension-RELEASE_1_1_1.tar.gz" https://github.com/tony2001/pinba_extension/archive/RELEASE_1_1_1.tar.gz \
    && tar -zxvf pinba_extension-RELEASE_1_1_1.tar.gz \
    && cd pinba_extension-RELEASE_1_1_1 \
    && phpize \
    && ./configure \
    && make install \
    && cd .. \
    && rm -rf pinba_extension-RELEASE_1_1_1.tar.gz pinba_extension-RELEASE_1_1_1 \
    && docker-php-ext-enable igbinary pinba memcached solr amqp\
    && docker-php-ext-install -j$(nproc) gettext opcache pdo pgsql pdo_pgsql intl zip gd bcmath \
    && curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer \
    && cd  / && rm -fr /src \
    && apk del build-dependencies \
    && rm -rf /tmp/*

RUN curl -sS https://getcomposer.org/installer | php
RUN mv composer.phar /usr/local/bin/composer


# Copy configuration
COPY configs/php.ini-development /usr/local/etc/php/
##COPY configs/amqp.ini /usr/local/etc/php/conf.d/
COPY configs/fpm/php-fpm.conf /usr/local/etc/
COPY configs/fpm/pool.d /usr/local/etc/pool.d

WORKDIR /var/www