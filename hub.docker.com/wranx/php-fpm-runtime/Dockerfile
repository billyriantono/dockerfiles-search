FROM php:7.3.11-fpm-stretch

# install the PHP extensions we need
RUN set -ex \
    && buildDeps=' \
        libjpeg62-turbo-dev \
        libgmp-dev \
        libpq-dev \
        re2c \
        libmhash-dev \
        libicu-dev \
        sqlite3 \
        libsqlite3-dev \
        file \
    ' \
    && mkdir -p /usr/share/man/man1 \
    && curl -sS -o /tmp/icu.tar.gz -L http://download.icu-project.org/files/icu4c/62.1/icu4c-62_1-src.tgz \
    && tar -zxf /tmp/icu.tar.gz -C /tmp \
    && cd /tmp/icu/source \
    && ./configure --prefix=/opt/icu \
    && make && make install \
    && apt-get update \
    && apt-get -y upgrade libicu-dev \
    && apt-get install -y --no-install-recommends $buildDeps libpng-dev libhiredis-dev libzip-dev mysql-client \
    && rm -rf /var/lib/apt/lists/* \
    && ln -s /usr/include/x86_64-linux-gnu/gmp.h /usr/local/include/ \
    && docker-php-ext-configure gd \
        --with-jpeg-dir=/usr \
        --with-png-dir=/usr \
    && docker-php-ext-configure gmp \
    && docker-php-ext-configure intl --with-icu-dir=/opt/icu \
    && docker-php-ext-install -j "$(nproc)" gd mbstring opcache pdo pdo_mysql pdo_sqlite pdo_pgsql zip intl gmp \
    && apt-mark manual \
        libjpeg62-turbo \
        libpq5 \
    && pecl install apcu \
    && echo "extension=apcu.so" > /usr/local/etc/php/conf.d/apcu.ini \
    && curl -sSL -o /tmp/phpiredis.tar.gz https://github.com/nrk/phpiredis/archive/v1.0.0.tar.gz \
    && tar -zxf /tmp/phpiredis.tar.gz -C /tmp \
    && cd /tmp/phpiredis-1.0.0 \
    && phpize && ./configure --enable-phpiredis \
    && make install \
    && echo "extension=phpiredis.so" > /usr/local/etc/php/conf.d/iredis.ini \
    && yes | pecl -C ./pear.conf install xdebug \
    && echo "zend_extension=$(find /usr/local/lib/php/extensions/ -name xdebug.so)" > /usr/local/etc/php/conf.d/xdebug.ini.off \
    && pecl install redis \
    && docker-php-ext-enable redis \
    && cd / && rm -Rf /tmp/* \
    && apt-get purge -y --auto-remove $buildDeps

# set recommended PHP.ini settings
# see https://secure.php.net/manual/en/opcache.installation.php
RUN { \
        echo 'opcache.memory_consumption=128'; \
        echo 'opcache.interned_strings_buffer=8'; \
        echo 'opcache.max_accelerated_files=4000'; \
        echo 'opcache.revalidate_freq=60'; \
        echo 'opcache.fast_shutdown=1'; \
        echo 'opcache.enable_cli=1'; \
    } > /usr/local/etc/php/conf.d/opcache-recommended.ini

# set upload size to 10M
RUN { \
        echo 'upload_max_filesize = 10M'; \
        echo 'post_max_size = 10M'; \
    } > /usr/local/etc/php/conf.d/upload-size.ini

