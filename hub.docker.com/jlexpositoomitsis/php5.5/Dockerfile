FROM php:5.5-fpm

# Container containing php-fpm and php-cli to run and interact with eZ Platform and other Symfony projects
#
# It has two modes of operation:
# - (run.sh cmd) [default] Reconfigure eZ Platform/Publish based on provided env variables and start php-fpm
# - (bash|php|composer) Allows to execute composer, php or bash against the image

# Set defaults for variables used by run.sh
ENV COMPOSER_HOME=/root/.composer \
    PHPREDIS_VERSION=2.2.8 \
    XDEBUG_VERSION=2.5.0 \
    PHPUNIT_VERSION=4.8

# Get packages that we need in container
RUN apt-get update -q -y \
    && apt-get install -q -y --force-yes --no-install-recommends \
        ca-certificates \
        curl \
        acl \
        sudo \
# Needed for the php extensions we enable below
        libfreetype6 \
        libjpeg62-turbo \
        libxpm4 \
        libpng12-0 \
        libicu52 \
        libxslt1.1 \
        libmcrypt-dev \
# git & unzip needed for composer, unless we document to use dev image for composer install
# unzip needed due to https://github.com/composer/composer/issues/4471
#        unzip \
#        git \
    && rm -rf /var/lib/apt/lists/*

# Install and configure php plugins
RUN set -xe \
    && buildDeps=" \
        $PHP_EXTRA_BUILD_DEPS \
        libfreetype6-dev \
        libjpeg62-turbo-dev \
        libxpm-dev \
        libpng12-dev \
        libicu-dev \
        libxslt1-dev \
    " \
    && apt-get update && apt-get install -y --force-yes $buildDeps --no-install-recommends && rm -rf /var/lib/apt/lists/* \
# Extract php source and install missing extensions
    && docker-php-source extract \
    && docker-php-ext-configure mysqli --with-mysqli=mysqlnd \
    && docker-php-ext-configure pdo_mysql --with-pdo-mysql=mysqlnd \
    && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ --with-png-dir=/usr/include/ --with-xpm-dir=/usr/include/ --enable-gd-native-ttf --enable-gd-jis-conv \
    && docker-php-ext-install exif gd mbstring intl xsl zip mysqli pdo_mysql soap zip mcrypt\
    && docker-php-ext-enable opcache \
    && cp /usr/src/php/php.ini-production ${PHP_INI_DIR}/php.ini \
    \
# Install redis
    && yes | pecl install redis-$PHPREDIS_VERSION \
    && echo "extension=redis.so" > ${PHP_INI_DIR}/conf.d/redis.ini \
    \
# Delete source & builds deps so it does not hang around in layers taking up space
    && docker-php-source delete \
    && apt-get purge -y --auto-remove -o APT::AutoRemove::RecommendsImportant=false $buildDeps

# Set timezone
RUN echo "UTC" > /etc/timezone && dpkg-reconfigure --frontend noninteractive tzdata \
    # Set pid file to be able to restart php-fpm
    && sed -i "s@^\[global\]@\[global\]\n\npid = /run/php-fpm.pid@" ${PHP_INI_DIR}-fpm.conf

#Install phpunit
RUN curl -Lo phpunit.phar "https://phar.phpunit.de/phpunit-${PHPUNIT_VERSION}.phar" \
    && chmod +x phpunit.phar \
    && mv phpunit.phar /usr/local/bin/phpunit

#Install xdebug
RUN mkdir -p /usr/src/xdebug \
    && curl -s -L "http://xdebug.org/files/xdebug-${XDEBUG_VERSION}.tgz" | tar -xvz -C /usr/src/xdebug --strip-components=1 \
    && cd /usr/src/xdebug \
    && phpize && ./configure --enable-xdebug && make && make install \
    && mkdir /usr/lib/php5/ && cp modules/xdebug.so /usr/lib/php5/xdebug.so

# Add some custom config
COPY conf.d/php.ini ${PHP_INI_DIR}/conf.d/php.ini
COPY conf.d/xdebug.ini ${PHP_INI_DIR}/conf.d/xdebug.ini


# Needed for docker-machine
#RUN usermod -u 1000 www-data

WORKDIR /var/www/html

#RUN chmod 755 /scripts/*.sh

# Create Composer directory (cache and auth files) & Get Composer
#RUN mkdir -p $COMPOSER_HOME \
#    && curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

#ENTRYPOINT ["/scripts/docker-entrypoint.sh"]

CMD php-fpm

EXPOSE 9000
