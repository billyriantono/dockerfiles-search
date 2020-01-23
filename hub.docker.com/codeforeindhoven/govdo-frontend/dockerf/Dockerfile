FROM php:7.3-cli-alpine3.9

LABEL maintainer Srdjan Vranac <vranac@gmail.com>

# persistent / runtime deps
ENV PHPIZE_DEPS \
    autoconf \
    cmake \
    file \
    g++ \
    gcc \
    libc-dev \
    make \
    git \
    pkgconf \
    re2c

# https://pkgs.alpinelinux.org/packages?name=&branch=&repo=&arch=&maintainer=
RUN apk update \
    && apk add --no-cache --virtual .build-deps \
            $PHPIZE_DEPS \
    && apk add git \
            bash \
            curl \
            icu \
            icu-libs \
            icu-dev \
            gettext-dev \
            postgresql-dev \
            icu-dev \
            freetype \
            libpng \
            libjpeg-turbo \
            freetype-dev \
            libpng-dev \
            libjpeg-turbo-dev \
            libxslt-dev \
            libxml2-dev \
            libsodium-dev \
            imagemagick \
            imagemagick-dev \
            libtool \
            pcre-dev
# Possible values for ext-name:
# bcmath bz2 calendar ctype curl dba dom enchant exif fileinfo filter ftp gd gettext
# gmp hash iconv imap interbase intl json ldap mbstring mysqli oci8 odbc opcache pcntl
# pdo pdo_dblib pdo_firebird pdo_mysql pdo_oci pdo_odbc pdo_pgsql pdo_sqlite pgsql phar posix
# pspell readline recode reflection session shmop simplexml snmp soap sockets sodium spl standard
# sysvmsg sysvsem sysvshm tidy tokenizer wddx xml xmlreader xmlrpc xmlwriter xsl zend_test zip

RUN docker-php-ext-configure gd \
    && docker-php-ext-install gd \
    && docker-php-ext-configure exif \
    && docker-php-ext-install exif \
    && docker-php-ext-configure pdo_mysql \
    && docker-php-ext-install pdo_mysql \
    && docker-php-ext-configure pdo_pgsql \
    && docker-php-ext-install pdo_pgsql \
    && docker-php-ext-configure intl \
    && docker-php-ext-install intl \
    && docker-php-ext-configure bcmath \
    && docker-php-ext-install bcmath \
    && docker-php-ext-configure xsl \
    && docker-php-ext-install xsl \
    && docker-php-ext-configure pcntl \
    && docker-php-ext-install pcntl \
    && docker-php-ext-configure opcache \
    && docker-php-ext-install opcache \
    && docker-php-ext-configure gettext \
    && docker-php-ext-install gettext \
    && docker-php-ext-configure iconv \
    && docker-php-ext-install iconv \
    && docker-php-ext-configure json \
    && docker-php-ext-install json \
    && docker-php-ext-configure mysqli \
    && docker-php-ext-install mysqli \
    && docker-php-ext-configure pgsql \
    && docker-php-ext-install pgsql \
    && docker-php-ext-configure sockets \
    && docker-php-ext-install sockets \
    && yes | pecl install xdebug-2.7.2 imagick-3.4.4 igbinary-3.0.1 redis-5.0.2 \
    && docker-php-ext-enable xdebug \
    && docker-php-ext-enable imagick \
    && docker-php-ext-enable igbinary redis \
    && rm -rf /var/cache/apk/* \
    # Install Composer
    && curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer \
    # Install Symfony installer
    &&  curl -sS https://get.symfony.com/cli/installer | bash \
    && mv /root/.symfony/bin/symfony /usr/local/bin/symfony \
    # create aliases
    && echo "alias php-debug='/usr/local/bin/php -dzend_extension=/usr/lib/php7/modules/xdebug.so'" >> ~/.bashrc \
    && echo "alias php-profiler='XDEBUG_CONFIG=\"profiler_enable=1\" /usr/local/bin/php -dzend_extension=/usr/lib/php7/modules/xdebug.so'" >> ~/.bashrc

ADD ./php-configuration/ /usr/local/etc/php/conf.d/
ADD ./php-xdebug/xdebug.ini ./php-xdebug/xdebug-profiler.ini /usr/local/etc/php/conf.d/

RUN mkdir -p /var/log/xdebug
RUN mkdir -p /var/log/xdebug/profiler_output
