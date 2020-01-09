FROM php:7.2-alpine

MAINTAINER Adriano Righi <contato@adrianorighi.com>

ENV LD_LIBRARY_PATH /opt/oci8/instantclient_12_1/

RUN apk update

# Install dev dependencies
RUN apk add --no-cache --virtual .build-deps \
    $PHPIZE_DEPS \
    curl-dev \
    imagemagick-dev \
    libtool \
    libxml2-dev \
    postgresql-dev \
    sqlite-dev \
    openldap-dev

# Install production dependencies
RUN apk add --no-cache \
    bash \
    curl \
    g++ \
    gcc \
    make \
    libaio-dev \
    git \
    imagemagick \
    libc-dev \
    libpng-dev \
    make \
    mysql-client \
    nodejs \
    nodejs-npm \
    yarn \
    openssh-client \
    postgresql-libs \
    rsync \
    zlib-dev \
    gcompat \
    libnsl \
    libzip-dev

# Install OCI8 Library
RUN ln -s /usr/lib/libnsl.so.2 /usr/lib/libnsl.so.1

RUN mkdir -p /opt/oci8

COPY ./oci8/instantclient-basic-linux.x64-12.1.0.2.0.zip /opt/oci8
COPY ./oci8/instantclient-sdk-linux.x64-12.1.0.2.0.zip /opt/oci8
COPY ./oci8/oci8-2.1.7.tgz /opt/oci8
RUN cd /opt/oci8 \
    && unzip instantclient-sdk-linux.x64-12.1.0.2.0.zip \
    && unzip instantclient-basic-linux.x64-12.1.0.2.0.zip \
    && cd instantclient_12_1/ \
    && ln -s libclntsh.so.12.1 libclntsh.so \
    && ln -s libocci.so.12.1 libocci.so \
    && cd ../ \
    && tar xzf oci8-2.1.7.tgz \
    && cd oci8-2.1.7 \
    && phpize \
    && ./configure --with-oci8=shared,instantclient,/opt/oci8/instantclient_12_1 \
    && make \
    && make install \
    && echo "extension=oci8.so" >> $PHP_INI_DIR/conf.d/oci8.ini \
    && cd /opt/oci8 \
    && rm *.zip \
    && rm *.tgz

# Install PECL and PEAR extensions
RUN pecl install \
    imagick

# Install and enable php extensions
RUN docker-php-ext-enable \
    imagick
RUN docker-php-ext-configure zip --with-libzip
RUN docker-php-ext-install \
    curl \
    iconv \
    mbstring \
    pdo \
    pdo_mysql \
    pdo_pgsql \
    pdo_sqlite \
    pcntl \
    tokenizer \
    xml \
    gd \
    zip \ 
    bcmath \
    ldap

# Install composer
ENV COMPOSER_HOME /composer
ENV PATH ./vendor/bin:/composer/vendor/bin:$PATH
ENV COMPOSER_ALLOW_SUPERUSER 1
RUN curl -s https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin/ --filename=composer

# Install PHP_CodeSniffer
RUN composer global require "squizlabs/php_codesniffer=*"

# Install Laravel Envoy
RUN composer global require "laravel/envoy"

# Cleanup dev dependencies
RUN apk del -f .build-deps

# Setup working directory
WORKDIR /var/www