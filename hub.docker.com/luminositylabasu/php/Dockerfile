FROM php:7.1-fpm

RUN echo 'deb http://security.debian.org/debian-security jessie/updates main' >> /etc/apt/sources.list.d/jessie.list
RUN apt-get update
RUN apt-get -o Acquire::ForceIPv4=true install -y libfreetype6-dev libjpeg62-turbo-dev libpng-dev \
                                                  mysql-client pv wget psmisc procps \
                                                  redis-tools curl git nano sudo \
                                                  software-properties-common libmcrypt-dev \
                                                  libmagickwand-dev zip iputils-ping \
                                                  libmemcached-dev libgmp-dev libuv1-dev \
                                                  libssl1.0.0 libssl-dev cron
# Choose PHP config
RUN cp /usr/local/etc/php/php.ini-development /usr/local/etc/php/php.ini
RUN rm /usr/local/etc/php/php.ini-production

# Install cassandra
WORKDIR /tmp
RUN wget -q http://downloads.datastax.com/cpp-driver/ubuntu/14.04/cassandra/v2.10.0/cassandra-cpp-driver_2.10.0-1_amd64.deb
RUN wget -q http://downloads.datastax.com/cpp-driver/ubuntu/14.04/cassandra/v2.10.0/cassandra-cpp-driver-dev_2.10.0-1_amd64.deb
RUN dpkg -i cassandra-cpp-driver_2.10.0-1_amd64.deb
RUN dpkg -i cassandra-cpp-driver-dev_2.10.0-1_amd64.deb

RUN pecl install cassandra
RUN docker-php-ext-enable cassandra

# Install imagick
RUN pecl install imagick
RUN docker-php-ext-enable imagick

# Install gd
RUN docker-php-ext-configure gd \
        --enable-gd-native-ttf \
        --with-jpeg-dir=/usr/lib \
        --with-freetype-dir=/usr/include/freetype2 && \
    docker-php-ext-install gd

# Install memcached
RUN pecl install memcached
RUN docker-php-ext-enable memcached

# Install mongo
RUN pecl install mongodb
RUN docker-php-ext-enable mongodb

# Install
RUN docker-php-ext-configure opcache --enable-opcache
RUN docker-php-ext-install opcache
COPY config/opcache.ini $PHP_INI_DIR/conf.d/

# Install EXT
RUN docker-php-ext-install -j$(nproc) iconv
RUN docker-php-ext-install bcmath
RUN docker-php-ext-install pcntl
RUN docker-php-ext-install pdo_mysql
RUN docker-php-ext-install soap
RUN docker-php-ext-install zip

# Custom DEV Config
COPY config/laravel.ini $PHP_INI_DIR/conf.d/

# Install composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

WORKDIR /var/www
