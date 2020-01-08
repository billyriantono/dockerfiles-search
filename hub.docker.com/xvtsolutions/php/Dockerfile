FROM webdevops/php-apache:7.1

ENV bamboo_uid 1001
ENV bamboo_gid 1001

# List of ENV variables that can be passed in a run time.
ARG DB_DRIVER
ARG DB_NAMESPACE
ARG DB_NAME
ARG DB_USER
ARG DB_PASS
ARG DB_HOST
ARG INSTALL_PROFILE

# Set uid and gid of user www-data to match with the bamboo user who starts the
# docker-compose command
RUN groupmod -g ${bamboo_gid} www-data && \
    usermod -g ${bamboo_gid} -u ${bamboo_uid} www-data && \
    chown -R www-data:www-data /var/www

# hack to make postgresql-client install work
RUN mkdir -p /usr/share/man/man1 \
    && mkdir -p /usr/share/man/man7

RUN apt-get update \
    && apt-get install -y -f\
        build-essential \
        git \
        zip \
        postgresql-client libpq-dev \
        libgmp-dev libfreetype6-dev \
        libjpeg62-turbo-dev libpng-dev

# Install GD
RUN docker-php-ext-configure gd \
    --with-freetype-dir=/usr/include/ \
    --with-png-dir=/usr/include/ \
    --with-jpeg-dir=/usr/include/ && \
  NPROC=$(getconf _NPROCESSORS_ONLN) && \
  docker-php-ext-install -j${NPROC} gd

# Install GMP
RUN ln -s /usr/include/x86_64-linux-gnu/gmp.h /usr/local/include/ && \
  docker-php-ext-configure gmp && \
  NPROC=$(getconf _NPROCESSORS_ONLN) && \
  docker-php-ext-install -j${NPROC} gmp

# Install additional PHP libraries
RUN NPROC=$(getconf _NPROCESSORS_ONLN) && \
  docker-php-ext-install -j${NPROC} bcmath pdo pdo_pgsql pdo_mysql opcache pcntl gmp zip

# Install libsodium
RUN curl -o /tmp/libsodium.tar.gz https://download.libsodium.org/libsodium/releases/libsodium-1.0.17.tar.gz && \
  tar -C /tmp -zxvf /tmp/libsodium.tar.gz && \
  rm /tmp/libsodium.tar.gz && \
  cd /tmp/libsodium-1.0.17 && \
  ./configure && \
  make && \
  make check && \
  make install && \
  pecl install libsodium && \
  docker-php-ext-enable sodium

# Install PHP APC
#RUN pecl install apcu-beta

# Install PhpRedis
RUN pecl install -o -f redis && \
    rm -rf /tmp/pear && \
    echo "extension=redis.so" > /usr/local/etc/php/conf.d/redis.ini

# Install hiredis
RUN apt-get install libhiredis-dev -y

# Build phpiredis
RUN cd /tmp && \
    git clone https://github.com/nrk/phpiredis.git phpiredis && \
    cd phpiredis && phpize && ./configure && make && make install && \
    echo 'extension=phpiredis.so' > /usr/local/etc/php/conf.d/33-phpiredis.ini

# Install composer and prestissimo
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer
RUN composer global require "hirak/prestissimo:^0.3" -vvv

RUN apt-get -y autoremove --purge build-essential && \
  apt-get -y autoremove && \
  apt-get -y clean && \
  rm -rf /var/lib/apt/lists/* && \
  rm -rf /tmp/*

COPY date-time.ini /usr/local/etc/php/conf.d/date-time.ini
COPY php-memory.ini /usr/local/etc/php/conf.d/php-memory.ini
COPY logs.ini /usr/local/etc/php/conf.d/logs.ini
