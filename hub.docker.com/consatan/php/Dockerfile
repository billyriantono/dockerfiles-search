FROM php:5.4-fpm

RUN apt-get update -y && \
    apt-get install -y --no-install-recommends \
        libfreetype6-dev \
        libjpeg62-turbo-dev \
        libmcrypt-dev \
        libpng12-dev \
        libgmp-dev \
        libxml2-dev \
        zlib1g-dev \
        libncurses5-dev \
        libmemcached-dev \
        libcurl4-openssl-dev \
        libssl-dev \
        php-pear \
        curl \
        wget && \
    rm -rf /var/lib/apt/lists/* && \
    ln -s /usr/include/x86_64-linux-gnu/gmp.h /usr/include/gmp.h && \
    docker-php-ext-configure pdo_mysql --with-pdo-mysql=mysqlnd && \
    docker-php-ext-install pdo_mysql && \
    docker-php-ext-configure mysql --with-mysql=mysqlnd && \
    docker-php-ext-install mysql && \
    docker-php-ext-configure mysqli --with-mysqli=mysqlnd && \
    docker-php-ext-install mysqli && \
    docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/lib && \
    docker-php-ext-install gd && \
    docker-php-ext-install soap && \
    docker-php-ext-install mcrypt && \
    docker-php-ext-install gmp && \
    docker-php-ext-install bcmath && \
    docker-php-ext-install mbstring && \
    docker-php-ext-install zip && \
    pecl install memcached-2.2.0 && \
    pecl install msgpack-0.5.7 && \
    pecl install apcu-4.0.11 && \
    pecl install redis && \
    pecl install yar && \
    pecl install xdebug-2.4.1 && \
    echo extension=memcached.so > /usr/local/etc/php/conf.d/memcached.ini && \
    echo extension=msgpack.so > /usr/local/etc/php/conf.d/msgpack.ini && \
    echo extension=apcu.so > /usr/local/etc/php/conf.d/apcu.ini && \
    echo extension=redis.so > /usr/local/etc/php/conf.d/redis.ini && \
    echo extension=yar.so > /usr/local/etc/php/conf.d/yar.ini && \
    echo zend_extension=/usr/local/lib/php/extensions/no-debug-non-zts-20100525/xdebug.so > /usr/local/etc/php/conf.d/xdebug.ini

CMD ["php-fpm"]
