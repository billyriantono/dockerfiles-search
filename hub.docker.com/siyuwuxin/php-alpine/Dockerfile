FROM php:7.3-fpm-alpine

LABEL Maintainer="Ansley Leung" \
      Description="latest PHP7 fpm Docker image. Use `docker-php-ext-install extension_name` to install Extensions." \
      License="MIT License" \
      Version="7.3.12"

# Environments
ENV TZ            Asia/Shanghai

# Set timezone
RUN set -ex && \
    apk update && \
    apk upgrade && \
    apk add --no-cache tzdata && \
    # ln -snf /usr/share/zoneinfo/ /etc/localtime && \
    cp /usr/share/zoneinfo/$TZ /etc/localtime && \
    echo $TZ > /etc/timezone && \
    apk del tzdata && \
    rm -rf /tmp/* /var/cache/apk/*

# Install extensions
RUN set -ex && \
    apk add --no-cache autoconf \
    build-base \
    curl \
    git \
    make \
    unzip \
    aspell-dev \
    bzip2-dev \
    curl-dev \
    freetype-dev \
    gettext-dev \
    icu-dev \
    imap-dev \
    krb5-dev \
    libbz2 \
    libjpeg-turbo-dev \
    libpng-dev \
    libwebp-dev \
    libxpm-dev \
    libstdc++ \
    libxml2-dev \
    libxslt-dev \
    libzip-dev \
    mysql-dev \
    net-snmp-dev \
    postgresql-dev \
    openldap-dev \
    openssl-dev && \
    : && \
    docker-php-ext-configure gd --with-webp-dir --with-jpeg-dir --with-png-dir \
        --with-zlib-dir --with-xpm-dir --with-freetype-dir && \
    docker-php-ext-install gd && \
    : && \
    docker-php-ext-configure imap --with-kerberos --with-imap-ssl && \
    docker-php-ext-install imap && \
    : && \
    docker-php-ext-configure ldap --with-libdir=lib/ && \
    docker-php-ext-install ldap && \
    : && \
    docker-php-ext-configure opcache --enable-opcache && \
    docker-php-ext-install opcache && \
    : && \
    docker-php-ext-configure zip --with-libzip && \
    docker-php-ext-install zip && \
    : && \
    docker-php-ext-install bcmath bz2 exif gettext intl mysqli pcntl pdo_mysql pdo_pgsql pspell && \
    : && \
    docker-php-ext-install shmop snmp soap sockets sysvmsg sysvsem sysvshm wddx xsl && \
    : && \
    rm -rf /tmp/* /var/cache/apk/*

# Set recommended opcache settings
# https://secure.php.net/manual/en/opcache.installation.php
RUN { \
            echo 'opcache.memory_consumption=128'; \
            echo 'opcache.interned_strings_buffer=8'; \
            echo 'opcache.max_accelerated_files=4000'; \
            echo 'opcache.revalidate_freq=60'; \
            echo 'opcache.fast_shutdown=1'; \
            echo 'opcache.enable_cli=1'; \
            echo 'opcache.file_cache=/tmp'; \
        } > $PHP_INI_DIR/conf.d/opcache-recommended.ini

# remove PHP version from the X-Powered-By HTTP header
# test: curl -I -H "Accept-Encoding: gzip, deflate" https://www.yourdomain.com
RUN echo 'expose_php = off' > $PHP_INI_DIR/conf.d/hide-header-version.ini

# Composer
RUN set -ex && \
    mkdir -p /usr/local/share/composer && \
    export COMPOSER_ALLOW_SUPERUSER=1 && \
    export COMPOSER_HOME=/usr/local/share/composer && \
    curl -sS https://install.phpcomposer.com/installer | php -- --install-dir=/usr/bin/ --filename=composer

# Install extension using pecl
# pecl install xdebug-beta
RUN set -ex && \
    apk add --no-cache imagemagick-dev \
    libmemcached-dev \
    pcre-dev && \
    : && \
    printf "\n" | pecl install imagick memcached mongodb oauth psr redis swoole xdebug && \
    docker-php-ext-enable imagick memcached mongodb oauth psr redis swoole xdebug && \
    : && \
    rm -rf /tmp/* /var/cache/apk/*

# PDFlib
# https://www.pdflib.com/download/pdflib-product-family/
RUN set -ex && \
    cd /tmp && \
    export PHP_EXT_DIR=$(php-config --extension-dir) && \
    curl -o pdflib.tar.gz https://www.pdflib.com/binaries/PDFlib/920/PDFlib-9.2.0-Alpine-Linux-x86_64-php.tar.gz -L && \
    tar -xvf pdflib.tar.gz && \
    mv PDFlib-* pdflib && cd pdflib && \
    cp bind/php/php-730-nts/php_pdflib.so $PHP_EXT_DIR && \
    docker-php-ext-enable php_pdflib && \
    cd /tmp && \
    rm -rf /tmp/*
