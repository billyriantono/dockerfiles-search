FROM php:7.2-fpm-alpine

COPY ./extensions /tmp/extensions

WORKDIR /tmp/extensions

RUN set -ex && apk add --no-cache linux-headers

RUN set -ex && apk --update --no-cache add linux-headers git curl zip unzip && \
    curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/bin --filename=composer

# pdo_firebird
RUN set -ex && \
    apk add --no-cache libbz2 libjpeg-turbo libpng gmp libintl c-client icu-libs libldap libpq aspell-libs net-snmp-libs tidyhtml-libs libxslt unixodbc freetds && \
    apk add --no-cache --virtual .build-deps-a autoconf g++ libtool make \
        curl-dev libxml2-dev icu-dev libxslt-dev net-snmp-dev \
        tidyhtml-dev gmp-dev openldap-dev readline-dev libedit-dev \
        postgresql-dev bzip2-dev aspell-dev aspell-en ldb-dev imap-dev \
        freetype-dev libjpeg-turbo-dev libpng-dev unixodbc-dev freetds-dev gettext-dev && \
    docker-php-ext-install pdo_mysql zip pcntl mysqli mbstring exif bcmath calendar \
        opcache sockets shmop sysvmsg sysvsem sysvshm dba soap curl gettext \
        pdo_pgsql pgsql intl bz2 xsl xmlrpc wddx snmp pspell tidy gmp ldap readline && \
    docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ && \
    docker-php-ext-install gd && \
    docker-php-ext-configure imap --with-imap --with-imap-ssl && \
    docker-php-ext-install imap && \
    docker-php-ext-configure pdo_odbc --with-pdo-odbc=unixODBC,/usr && \
    docker-php-ext-install pdo_odbc && \
    docker-php-ext-install pdo_dblib && \
     docker-php-source extract; \
        { \
                echo '# https://github.com/docker-library/php/issues/103#issuecomment-271413933'; \
                echo 'AC_DEFUN([PHP_ALWAYS_SHARED],[])dnl'; \
                echo; \
                cat /usr/src/php/ext/odbc/config.m4; \
        } > temp.m4; \
        mv temp.m4 /usr/src/php/ext/odbc/config.m4; \
    docker-php-ext-configure odbc --with-unixODBC=shared,/usr && \
    docker-php-ext-install odbc && \
    apk del .build-deps-a

RUN set -ex && \
    apk add --no-cache zlib file imagemagick-libs libmemcached-libs && \
    apk add --no-cache --virtual .build-deps-b autoconf g++ libtool make \
        file-dev libmemcached-dev imagemagick-dev zlib-dev unixodbc-dev && \
    printf "\n" | pecl install imagick-3.4.4 && \
    docker-php-ext-enable imagick && \
    #
    printf "\n" | pecl install yaf && \
    docker-php-ext-enable yaf && \
    printf "\n" | pecl install memcached-3.1.3 && \
    docker-php-ext-enable memcached && \
    #
    pecl install pdo_sqlsrv && \
    docker-php-ext-enable pdo_sqlsrv && \
    #
    printf "\n" | pecl install sqlsrv && \
    docker-php-ext-enable sqlsrv && \
    pecl install APCu-5.1.11 && \
    docker-php-ext-enable apcu && \
    apk del .build-deps-b

RUN set -ex && \
    apk add --no-cache rabbitmq-c && \
    apk add --no-cache --virtual .build-deps-c autoconf g++ libtool make rabbitmq-c-dev && \
    cd /tmp/extensions && \
    pecl install amqp-1.9.4.tgz && \
    docker-php-ext-enable amqp && \
    # redis
    mkdir redis && \
    tar -xf redis-4.1.1.tgz -C redis --strip-components=1 && \
    (cd redis && phpize && ./configure && make && make install) && \
    docker-php-ext-enable redis && \
    # swoole
    mkdir swoole && \
    tar -xf swoole-4.2.1.tgz -C swoole --strip-components=1 && \
    (cd swoole && phpize && ./configure --enable-openssl && make && make install) && \
    docker-php-ext-enable swoole && \
    # sg_loader
    wget https://www.sourceguardian.com/loaders/download/loaders.linux-x86_64.tar.gz -q -O sg_loader.tar.gz && \
    tar -zxf sg_loader.tar.gz && \
    cp ixed.7.2.lin "$(php -r 'echo ini_get("extension_dir");')/sg_loader.so" && \
    echo "extension=sg_loader.so" >/usr/local/etc/php/conf.d/docker-php-ext-sg11-loader.ini && \
    # ioncube_loader
    wget https://downloads.ioncube.com/loader_downloads/ioncube_loaders_lin_x86-64.tar.gz -q -O ioncube_loader.tar.gz && \
    tar -zxf ioncube_loader.tar.gz && \
    cp ioncube/ioncube_loader_lin_7.2.so "$(php -r 'echo ini_get("extension_dir");')/ioncube_loader.so" && \
    echo "zend_extension=ioncube_loader.so" >/usr/local/etc/php/conf.d/docker-php-ext-ioncube-loader.ini && \
    apk del .build-deps-c && \
    rm -rf /var/cache/apk/*

WORKDIR /home/wwwroot
