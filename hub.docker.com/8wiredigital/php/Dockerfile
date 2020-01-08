FROM debian:jessie

MAINTAINER 8 Wire Digital <info@8wiredigital.co.nz>

ENV PHP_MAJOR_VERSION=7 \
    PHP_MINOR_VERSION=2 \
    PHP_PATCH_VERSION=25 \
    PHP_USER=www \
    PHP_USERID=9999 \
    PHP_INI_DIR=/etc \
    PHPREDIS_VERSION=5.1.1 \
    SRC_DIR=/tmp/src \
    EXTENSION_DIR=/usr/local/lib/php/extensions \
    ## -- to generate - define dependancies \
    PERSISTANT_DEPS="\
        cron \
        ca-certificates \
        curl \
        ssmtp \
        libjpeg62-turbo \
        libpng12-0 \
        libxml2 \
        librecode0 \
        libsqlite3-0 \
        libxslt1.1 \
        libicu-dev \
        libmcrypt4 \
        patch \
        file \
        mysql-client \
        libfreetype6 \
        unzip \
        zip \
        nano-tiny" \
    BUILD_DEPS=" \
        libpcre3-dev \
        zlib1g-dev \
        autoconf \
        g++ \
        gcc \
        libc-dev \
        make \
        pkg-config \
        re2c \
        libcurl4-openssl-dev \
        libreadline6-dev \
        librecode-dev \
        libsqlite3-dev \
        libssl-dev \
        xz-utils \
        libjpeg62-turbo-dev \
        libpng12-dev \
        libmcrypt-dev \
        libxml2-dev \
        bison \
        libxslt1-dev \
        libfreetype6-dev" \
    GPG_KEYS="1729F83938DA44E27BA0F4D3DBDB397470D12172 B1B44D8F021E4E2D6021E995DC9FF8D3EE5AF27F" \
    PHP_SHA256=746efeedc38e6ff7b1ec1432440f5fa801537adf6cd21e4afb3f040e5b0760a9

RUN useradd -m -u ${PHP_USERID} ${PHP_USER}

#set up config and log directories
RUN mkdir -p $PHP_INI_DIR/php.d \
    mkdir -p $PHP_INI_DIR/php-fpm.d \
    mkdir -p /var/log/php


RUN set -xe \
    && for key in $GPG_KEYS; do \
        gpg --batch --keyserver keys.gnupg.net --recv-keys "$key"; \
    done


COPY docker-php-ext-* /usr/local/bin/

# point apt to local cache to speed up local builds
# RUN  echo 'Acquire::http { Proxy "http://192.168.0.100:3142"; };' >> /etc/apt/apt.conf.d/01proxy

RUN set -xe \
    ## -- to generate - clean package manager
    && apt-get update && apt-get install -y $BUILD_DEPS $PERSISTANT_DEPS --no-install-recommends && rm -rf /var/lib/apt/lists/* \
    ## -- end to generate

    # create and move too temp dir
    && mkdir -p ${SRC_DIR} \
    && cd ${SRC_DIR} \

    # get required php version and check
    && curl -fSL "http://php.net/get/php-$PHP_MAJOR_VERSION.$PHP_MINOR_VERSION.$PHP_PATCH_VERSION.tar.xz/from/this/mirror" -o php.tar.xz \
    && echo "$PHP_SHA256 *php.tar.xz" | sha256sum -c - \
    && curl -fSL "http://php.net/get/php-$PHP_MAJOR_VERSION.$PHP_MINOR_VERSION.$PHP_PATCH_VERSION.tar.xz.asc/from/this/mirror" -o php.tar.xz.asc \
    && export GNUPGHOME="$(mktemp -d)" \
    && for key in $GPG_KEYS; do \
        gpg --keyserver ha.pool.sks-keyservers.net --recv-keys "$key"; \
    done \
    && gpg --batch --verify php.tar.xz.asc php.tar.xz \
    && rm -r "$GNUPGHOME" \
    && mkdir ${SRC_DIR}/php \
    && tar -Jxf php.tar.xz -C ${SRC_DIR}/php --strip-components=1 \
    && cd ${SRC_DIR} \

    # install php extensions from source
    # download and prepare redis extension
    && curl -L -o redis.tar.gz https://github.com/phpredis/phpredis/archive/$PHPREDIS_VERSION.tar.gz \
    && tar xfz redis.tar.gz \
    && mv phpredis-$PHPREDIS_VERSION ${SRC_DIR}/php/ext/redis \


    # configure php
    && cd ${SRC_DIR}/php \
    && ./configure --with-config-file-path="$PHP_INI_DIR" \
        --build=$CBUILD \
        --host=$CHOST \
        --with-config-file-scan-dir="$PHP_INI_DIR/php.d" \
        --with-fpm-user=$PHP_USER \
        --with-fpm-group=$PHP_USER \
        --disable-cgi \
        --enable-fpm \
        --enable-mysqlnd \
        --enable-soap \
        --enable-zip \
        --enable-mbstring \
        --enable-intl \
        --enable-opcache \
        --enable-pcntl \
        --enable-ftp \
        --with-iconv-dir=/usr/bin \
        --with-xsl \
        --with-curl \
        --with-gd \
        --with-openssl \
        --with-zlib \
        --with-pdo-mysql \
        --with-mysqli \
        --with-mcrypt \
        --with-mysql-sock=/var/mysql/mysql.sock \
        --with-jpeg-dir=/usr/lib/x86_64-linux-gnu/ \
        --with-freetype-dir=/usr/lib/x86_64-linux-gnu/ \
        --with-png-dir=/usr/lib/x86_64-linux-gnu/ \
        --enable-exif \
        --enable-bcmath \
    \
    && make -j"$(getconf _NPROCESSORS_ONLN)" \
    && make install \
    && make clean \
    \

    # install precompiled php extensions

    #ioncube
    && cd ${SRC_DIR} \
    && curl -o ${SRC_DIR}/ioncube.tar.gz http://downloads3.ioncube.com/loader_downloads/ioncube_loaders_lin_x86-64.tar.gz \
    && export VERSION=`php -r "echo PHP_MAJOR_VERSION.'.'.PHP_MINOR_VERSION;"`\
    && tar zxpf ${SRC_DIR}/ioncube.tar.gz -C ${SRC_DIR}\
    #temp for php 7 beta
    # && curl -o ${SRC_DIR}/php7-linux-x86-64-beta7.tgz https://www.ioncube.com/php7-linux-x86-64-beta7.tgz \
    # && tar zxpf ${SRC_DIR}/php7-linux-x86-64-beta7.tgz -C ${SRC_DIR}/ioncube \
    #&& mv ${SRC_DIR}/ioncube/ioncube_loader_lin_${VERSION}.so `php -r "echo ini_get('extension_dir');"`/ioncube_loader_lin_${VERSION}.so \
    && mv ${SRC_DIR}/ioncube/ioncube_loader_lin_${VERSION}.so `php -r "echo ini_get('extension_dir');"`/ioncube.so \

    # blackfire
    && export VERSION=`php -r "echo PHP_MAJOR_VERSION.PHP_MINOR_VERSION;"` \
    && curl -A "Docker" -o ${SRC_DIR}/blackfire-probe.tar.gz -D - -L -s https://blackfire.io/api/v1/releases/probe/php/linux/amd64/${VERSION} \
    && tar zxpf ${SRC_DIR}/blackfire-probe.tar.gz -C ${SRC_DIR} \
    && mv ${SRC_DIR}/blackfire-*.so `php -r "echo ini_get('extension_dir');"`/blackfire.so \


    # # download precompiled php extenstions for ioncube and blackfire
    # # download source and compile redis
    # # ioncube
    # && curl http://downloads3.ioncube.com/loader_downloads/ioncube_loaders_lin_x86-64.tar.gz > ioncube.tar.gz \
    # && export VERSION=`php -r "echo PHP_MAJOR_VERSION.'.'.PHP_MINOR_VERSION;"`\
    # && tar xzf ioncube.tar.gz \
    # && mv ioncube/ioncube_loader_lin_${VERSION}.so `php -r "echo ini_get('extension_dir');"`/ioncube_loader_lin_${VERSION}.so \
    # && rm -f ioncube.tar.gz && rm -rf ioncube \
    # # blackfire
    # && export VERSION=`php -r "echo PHP_MAJOR_VERSION.PHP_MINOR_VERSION;"` \
    # && curl -A "Docker" -o /tmp/blackfire-probe.tar.gz -D - -L -s https://blackfire.io/api/v1/releases/probe/php/linux/amd64/${VERSION} \
    # && tar zxpf /tmp/blackfire-probe.tar.gz -C /tmp \
    # && mv /tmp/blackfire-*.so `php -r "echo ini_get('extension_dir');"`/blackfire.so \
    # && rm -f /tmp/blackfire-probe.tar.gz \
    # # redis
    # && curl -L -o /tmp/redis.tar.gz https://github.com/phpredis/phpredis/archive/$PHPREDIS_VERSION.tar.gz \
    # && tar xfz /tmp/redis.tar.gz \
    # && rm -r /tmp/redis.tar.gz \
    # && mv phpredis-$PHPREDIS_VERSION /usr/src/php/ext/redis \
    # \
    # #install and configure additional extensions
    && docker-php-ext-install redis \
    && docker-php-ext-enable opcache \

    \
    # Tidy up dependencies and downloaded source code
    && strip -s /usr/local/bin/php \
    && strip -s /usr/local/sbin/php-fpm \

    ## -- to generate - clean package manager
    && { find /usr/local/bin /usr/local/sbin -type f -executable -exec strip --strip-all '{}' + || true; } \
    && apt-get purge -y --auto-remove -o APT::AutoRemove::RecommendsImportant=false -o APT::AutoRemove::SuggestsImportant=false $BUILD_DEPS \
    ## -- end to generate

    && cd / \
    && rm -rf ${SRC_DIR} \;

#HACK - This shouldn't be needed again
RUN apt-get update && apt-get install -y $PERSISTANT_DEPS --no-install-recommends && rm -rf /var/lib/apt/lists/*


#install composer, magerun, phpcpd
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer \

    && curl -o /usr/local/bin/magerun http://files.magerun.net/n98-magerun-latest.phar \
    && chmod +x /usr/local/bin/magerun \
    && curl -o /usr/local/bin/magerun2 https://files.magerun.net/n98-magerun2.phar \
    && chmod +x /usr/local/bin/magerun2

    #&& curl -O https://phar.phpunit.de/phpcpd.phar && chmod +x phpcpd.phar && mv phpcpd.phar /usr/local/bin/phpcpd;


COPY conf/php.ini ${PHP_INI_DIR}/
COPY conf/php-fpm.conf ${PHP_INI_DIR}/
COPY conf/www.conf ${PHP_INI_DIR}/php-fpm.d/
COPY conf/cron-www /tmp/crontab/www
# see https://stackoverflow.com/questions/43022296/crons-in-cron-d-wont-run-on-ubuntu-running-inside-docker-container
COPY conf/pam.d /etc/pam.d/cron


COPY bin/cronstart /usr/bin/cronstart
RUN chmod +x /usr/bin/cronstart

EXPOSE 9000
# CMD ["/usr/bin/start"]
CMD ["php-fpm", "-F", "-y", "/etc/php-fpm.conf"]

#CMD
