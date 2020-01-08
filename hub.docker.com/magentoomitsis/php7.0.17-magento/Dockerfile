FROM php:7.0.17-fpm
ENV XDEBUG_VERSION=2.5.0

#IMAGE DEPENDENCIES
    #CRON NEEDED TO ADD WEB CRONTABS
    #MYSQL-CLIENT NEEDED FOR MAGERUN
ENV ImageDeps="\
    cron \
    mysql-client \
    git \
"

# Install PHP7
RUN buildDeps=" \
        libpng12-dev \
        libjpeg-dev \
        libmcrypt-dev \
        libxml2-dev \
        freetype* \
        libxslt1-dev \
        cron \
        libicu-dev \
    "; \
    set -x \
    && apt-get update && apt-get install -y $ImageDeps $buildDeps --no-install-recommends && rm -rf /var/lib/apt/lists/* \
    && docker-php-ext-configure \
    gd --with-png-dir=/usr --with-jpeg-dir=/usr --with-freetype-dir \
    && docker-php-ext-install -j "$(getconf _NPROCESSORS_ONLN)" \
    gd \
    mbstring \
    mysqli \
    mcrypt \
    pdo_mysql \
    soap \
    zip \
    bcmath \
    intl \
    xsl \
    && curl -s -L "http://xdebug.org/files/xdebug-${XDEBUG_VERSION}.tgz" | tar -xvz -C /tmp \
    && cd "/tmp/xdebug-${XDEBUG_VERSION}/" \
    && phpize && ./configure --enable-xdebug && make \
    && mkdir /usr/lib/php7/ && cp modules/xdebug.so /usr/lib/php7/xdebug.so \
    && touch /usr/local/etc/php/ext-xdebug.ini \
    && curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer \
    && adduser --disabled-password --gecos "" magento \


    # Purge and delete tmp folders to reduce image size
    && apt-get purge -y --auto-remove \
    && rm -rf /tmp/*

# Configure PHP
COPY php.ini /usr/local/etc/php/php.ini
COPY php-fpm.conf /usr/local/etc/
COPY ext-xdebug.ini /usr/local/etc/php/conf.d/ext-xdebug.ini

ENV PHP_IDE_CONFIG="serverName=localhost"