# Use phusion/baseimage as base image. To make your builds reproducible, make
# sure you lock down to a specific version, not to `latest`!
# See https://github.com/phusion/baseimage-docker/blob/master/Changelog.md for
# a list of version numbers.
FROM phusion/baseimage:0.9.19
MAINTAINER Adi Priyanto <adipriyanto.bpn@gmail.com>
ENV REFRESHED_AT 2016-09-14

# Usage of ENV DEBIAN_FRONTEND noninteractive should be actively discouraged.
# The new ARG directive in the Dockerfile can set this only during the build.
# source : https://github.com/docker/docker/issues/4032
ARG TERM=linux
ARG DEBIAN_FRONTEND=noninteractive
ENV TERM=linux
ENV DEBIAN_FRONTEND=noninteractive

# Use baseimage-docker's init system.
CMD ["/sbin/my_init"]

# -- Using Indonesian Ubuntu Repository
# source : 
# - https://help.ubuntu.com/community/IndonesianLocalSourcesList
# - http://kambing.ui.ac.id/status/
RUN cp /etc/apt/sources.list /etc/apt/sources.list.bak \
    && sed -i 's/archive.ubuntu.com/kambing.ui.ac.id/g' /etc/apt/sources.list \
    && apt-get update \
    && apt-get install -y \
        wget \
        nano \
    --no-install-suggests \
    --no-install-recommends

# -- Login to the container, or running a command inside it, via SSH --
RUN rm -f /etc/service/sshd/down
ADD ssh/id_rsa.pub /tmp/your_key.pub
RUN cat /tmp/your_key.pub >> /root/.ssh/authorized_keys && rm -f /tmp/your_key.pub
EXPOSE 22

#-------------------------------------------------------------------------------
# ...put your own build instructions here...

# this script is based on php:7.0.10-apache
# source :
#   https://github.com/docker-library/php/blob/2f96a00aaa90ee1c503140724936ca7005273df5/7.0/apache/Dockerfile

# persistent / runtime deps
ENV PHPIZE_DEPS \
        autoconf \
        file \
        g++ \
        gcc \
        libc-dev \
        make \
        pkg-config \
        re2c

ENV PHP_INI_DIR /usr/local/etc/php

ENV APACHE_CONFDIR /etc/apache2
ENV APACHE_ENVVARS $APACHE_CONFDIR/envvars

ENV PHP_EXTRA_BUILD_DEPS apache2-dev
ENV PHP_EXTRA_CONFIGURE_ARGS --with-apxs2

ENV GPG_KEYS 1A4E8B7277C42E53DBA9C7B9BCAA30EA9C0D5763

ENV PHP_VERSION 7.0.10
ENV PHP_FILENAME php-7.0.10.tar.xz
ENV PHP_SHA256 348476ff7ba8d95a1e28e1059430c10470c5f8110f6d9133d30153dda4cdf56a

COPY docker-php-source /usr/local/bin/

COPY docker-php-ext-* /usr/local/bin/

# --- EXTENSION LIST ---
#
#   note : generated using https://ozh.github.io/ascii-tables/
#
#   +--------------------+------------------------------+--------------------+------------------+
#   | Enabled by Default | Available in PHP Source Code | Should be Disabled | Can be Installed |
#   +--------------------+------------------------------+--------------------+------------------+
#   |                    | bcmath                       |                    | bcmath           |
#   |                    | bz2                          |                    | bz2              |
#   |                    | calendar                     |                    | calendar         |
#   | core               |                              |                    |                  |
#   | ctype              | ctype                        |                    |                  |
#   | curl               | curl                         |                    |                  |
#   | date               |                              |                    |                  |
#   |                    | dba                          |                    | dba              |
#   | dom                | dom                          |                    |                  |
#   |                    | enchant                      |                    | enchant          |
#   |                    | exif                         |                    | exif             |
#   | fileinfo           | fileinfo                     |                    |                  |
#   | filter             | filter                       |                    |                  |
#   | ftp                | ftp                          |                    |                  |
#   |                    | gd                           |                    | gd               |
#   |                    | gettext                      |                    | gettext          |
#   |                    | gmp                          |                    | gmp              |
#   | hash               | hash                         |                    |                  |
#   | iconv              | iconv                        |                    |                  |
#   |                    | imap                         |                    | imap             |
#   |                    | interbase                    |                    | interbase        |
#   |                    | intl                         |                    | intl             |
#   | json               | json                         |                    |                  |
#   |                    | ldap                         |                    | ldap             |
#   | libxml             |                              |                    |                  |
#   | mbstring           | mbstring                     |                    |                  |
#   |                    | mcrypt                       |                    | mcrypt           |
#   |                    | mysqli                       |                    | mysqli           |
#   | mysqlnd            |                              |                    |                  |
#   |                    | oci8                         |                    | oci8             |
#   |                    | odbc                         | odbc               |                  |
#   |                    | opcache                      |                    | opcache          |
#   | openssl            |                              |                    |                  |
#   |                    | pcntl                        |                    | pcntl            |
#   | pcre               |                              |                    |                  |
#   | pdo                | pdo                          |                    |                  |
#   |                    | pdo_dblib                    |                    | pdo_dblib        |
#   |                    | pdo_firebird                 |                    | pdo_firebird     |
#   |                    | pdo_mysql                    |                    | pdo_mysql        |
#   |                    | pdo_oci                      |                    | pdo_oci          |
#   |                    | pdo_odbc                     |                    | pdo_odbc         |
#   |                    | pdo_pgsql                    |                    | pdo_pgsql        |
#   | pdo_sqlite         | pdo_sqlite                   |                    |                  |
#   |                    | pgsql                        |                    | pgsql            |
#   | phar               | phar                         |                    |                  |
#   | posix              | posix                        |                    |                  |
#   |                    | pspell                       |                    | pspell           |
#   | readline           | readline                     |                    |                  |
#   |                    | recode                       |                    | recode           |
#   | reflection         | reflection                   |                    |                  |
#   | session            | session                      |                    |                  |
#   |                    | shmop                        |                    | shmop            |
#   | simplexml          | simplexml                    |                    |                  |
#   |                    | snmp                         | snmp               |                  |
#   |                    | soap                         |                    | soap             |
#   |                    | sockets                      |                    | sockets          |
#   | spl                | spl                          |                    |                  |
#   | sqlite3            |                              |                    |                  |
#   | standard           | standard                     |                    |                  |
#   |                    | sysvmsg                      |                    | sysvmsg          |
#   |                    | sysvsem                      |                    | sysvsem          |
#   |                    | sysvshm                      |                    | sysvshm          |
#   |                    | tidy                         |                    | tidy             |
#   | tokenizer          | tokenizer                    |                    |                  |
#   |                    | wddx                         |                    | wddx             |
#   | xml                | xml                          |                    |                  |
#   | xmlreader          | xmlreader                    |                    |                  |
#   |                    | xmlrpc                       |                    | xmlrpc           |
#   | xmlwriter          | xmlwriter                    |                    |                  |
#   |                    | xsl                          |                    | xsl              |
#   |                    | zip                          |                    | zip              |
#   | zlib               |                              |                    |                  |
#   +--------------------+------------------------------+--------------------+------------------+

COPY oracle-client /tmp

ENV PHP_EXTS \
        bcmath \
        bz2 \
        calendar \
        dba \
        enchant \
        exif \
        gd \
        gettext \
        gmp \
        imap \
        interbase \
        intl \
        ldap \
        mcrypt \
        mysqli \
        oci8 \
        opcache \
        pcntl \
        pdo_dblib \
        pdo_firebird \
        pdo_mysql \
        pdo_oci \
        pdo_odbc \
        pdo_pgsql \
        pgsql \
        pspell \
        recode \
        shmop \
        soap \
        sockets \
        sysvmsg \
        sysvsem \
        sysvshm \
        tidy \
        wddx \
        xmlrpc \
        xsl \
        zip

ENV PHP_EXTS_BUILD_DEPS \
# ext-bz2
        libbz2-dev \
# ext-enchant
        libenchant-dev \
# ext-gd
        libpng12-dev libjpeg62-dev libfreetype6-dev zlib1g-dev libwebp-dev \
# ext-gmp
        libgmp3-dev \
# ext-imap
        libc-client-dev libkrb5-dev \
# ext-interbase ext-pdo_firebird
        firebird-dev \
# ext-intl
        libicu-dev \
# ext-ldap
        libldap2-dev \
# ext-mcrypt
        libmcrypt-dev \
# ext-pdo_dblib
        freetds-dev \
# ext-oci8 ext-pdo_oci
        libaio-dev \
# ext-pdo_odbc
        unixodbc-dev \
# ext-pdo_pgsql
        libpq-dev postgresql-server-dev-all \
# ext-pspell
        libpspell-dev \
# ext-recode
        librecode-dev \
# ext-soap ext-wddx ext-xmlrpc
        libxml2-dev \
# ext-tidy
        libtidy-dev \
# ext-xsl
        libxslt1-dev

RUN chmod +x /usr/local/bin/docker-php-source \
    && chmod +x /usr/local/bin/docker-php-ext-* \
    \
    \
    \
# ---------------------------------------
# -- install & configure Apache2 + PHP --
# ---------------------------------------
    \
    && apt-get install -y \
        $PHPIZE_DEPS \
        $PHP_EXTS_BUILD_DEPS \
        ca-certificates \
        curl \
        libedit2 \
        libsqlite3-0 \
        libxml2 \
        xz-utils \
    --no-install-recommends \
    \
    && mkdir -p $PHP_INI_DIR/conf.d \
    \
    && apt-get install -y \
        apache2 \
    --no-install-recommends \
    \
    && set -ex \
    \
# generically convert lines like
#   export APACHE_RUN_USER=www-data
# into
#   : ${APACHE_RUN_USER:=www-data}
#   export APACHE_RUN_USER
# so that they can be overridden at runtime ("-e APACHE_RUN_USER=...")
    && sed -ri 's/^export ([^=]+)=(.*)$/: ${\1:=\2}\nexport \1/' "$APACHE_ENVVARS" \
    \
# setup directories and permissions
    && . "$APACHE_ENVVARS" \
    && for dir in \
        "$APACHE_LOCK_DIR" \
        "$APACHE_RUN_DIR" \
        "$APACHE_LOG_DIR" \
        /var/www/html \
    ; do \
        rm -rvf "$dir" \
        && mkdir -p "$dir" \
        && chown -R "$APACHE_RUN_USER:$APACHE_RUN_GROUP" "$dir"; \
    done \
    \
# Apache + PHP requires preforking Apache for best results
    && a2dismod mpm_event && a2enmod mpm_prefork \
    \
# logs should go to stdout / stderr
    && . "$APACHE_ENVVARS" \
    && ln -sfT /dev/stderr "$APACHE_LOG_DIR/error.log" \
    && ln -sfT /dev/stdout "$APACHE_LOG_DIR/access.log" \
    && ln -sfT /dev/stdout "$APACHE_LOG_DIR/other_vhosts_access.log" \
    \
# PHP files should be handled by PHP, and should be preferred over any other file type
    && { \
        echo '<FilesMatch \.php$>'; \
        echo '\tSetHandler application/x-httpd-php'; \
        echo '</FilesMatch>'; \
        echo; \
        echo 'DirectoryIndex disabled'; \
        echo 'DirectoryIndex index.php index.html'; \
        echo; \
        echo '<Directory /var/www/>'; \
        echo '\tOptions -Indexes'; \
        echo '\tAllowOverride All'; \
        echo '</Directory>'; \
    } | tee "$APACHE_CONFDIR/conf-available/docker-php.conf" \
    && a2enconf docker-php \
    \
    && cd /usr/src \
    && curl -fSL "https://secure.php.net/get/$PHP_FILENAME/from/this/mirror" -o php.tar.xz \
    && echo "$PHP_SHA256 *php.tar.xz" | sha256sum -c - \
    && curl -fSL "https://secure.php.net/get/$PHP_FILENAME.asc/from/this/mirror" -o php.tar.xz.asc \
    && export GNUPGHOME="$(mktemp -d)" \
    && for key in $GPG_KEYS; do \
        gpg --keyserver ha.pool.sks-keyservers.net --recv-keys "$key"; \
    done \
    && gpg --batch --verify php.tar.xz.asc php.tar.xz \
    && rm -r "$GNUPGHOME" \
    \
    && buildDeps=" \
        $PHP_EXTRA_BUILD_DEPS \
        libedit-dev \
        libsqlite3-dev \
        libssl-dev \
        libxml2-dev \
    " \
    && apt-get install -y \
        $buildDeps \
# -- libcurl.so.4 shared object is needed by libphp7.so (so, don't remove it)
        libcurl4-openssl-dev \
    --no-install-recommends \
    \
    && docker-php-source extract \
    && cd /usr/src/php \
    && ./configure \
        --with-config-file-path="$PHP_INI_DIR" \
        --with-config-file-scan-dir="$PHP_INI_DIR/conf.d" \
        \
        --disable-cgi \
        \
# --enable-ftp is included here because ftp_ssl_connect() needs ftp to be compiled statically (see https://github.com/docker-library/php/issues/236)
        --enable-ftp \
# --enable-mbstring is included here because otherwise there's no way to get pecl to use it properly (see https://github.com/docker-library/php/issues/195)
        --enable-mbstring \
# --enable-mysqlnd is included here because it's harder to compile after the fact than extensions are (since it's a plugin for several extensions, not an extension in itself)
        --enable-mysqlnd \
        \
        --with-curl \
        --with-libedit \
        --with-openssl \
        --with-zlib \
        \
        $PHP_EXTRA_CONFIGURE_ARGS \
    && make -j"$(nproc)" \
    && make install \
    && { find /usr/local/bin /usr/local/sbin -type f -executable -exec strip --strip-all '{}' + || true; } \
    && make clean \
    && docker-php-source delete \
    \
    \
    \
# ----------------------------------------
# -- configure & install PHP extensions --
# ----------------------------------------
    \
# ext-gd
    && docker-php-ext-configure gd \
        --enable-gd-native-ttf \
        --with-jpeg-dir=/usr/include \
        --with-freetype-dir=/usr/include \
        --with-png-dir=/usr/include \
        --with-webp-dir=/usr/include \
# ext-gmp
    && ln -s /usr/include/x86_64-linux-gnu/gmp.h /usr/include/ \
# ext-ldap
    && ln -s /usr/lib/x86_64-linux-gnu/libldap.so /usr/lib/ \
# ext-interbase ext-pdo_firebird
    && ln -s /usr/lib64/libtds.so /usr/lib/ \
# ext-imap
    && docker-php-ext-configure imap \
        --with-kerberos \
        --with-imap-ssl \
# ext-pdo_dblib
    && ln -s /usr/lib/x86_64-linux-gnu/libsybdb.so.5.0.0 /usr/lib/libsybdb.so \
# ext-pdo_oci
    && cd /tmp \
    && dpkg -i oracle-instantclient12.1-basiclite_12.1.0.2.0-2_amd64.deb \
    && dpkg -i oracle-instantclient12.1-devel_12.1.0.2.0-2_amd64.deb \
    && docker-php-ext-configure pdo_oci \
        --with-pdo-oci=instantclient,/usr,12.1 \
# ext-pdo_odbc
    && docker-php-ext-configure pdo_odbc \
        --with-pdo-odbc=unixODBC,/usr \
    \
    && docker-php-ext-install -j"$(nproc)" $PHP_EXTS \
    && docker-php-source delete \
    \
    \
    \
    && apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

# -----------------------------
# -- prepare apache2 service --
# -----------------------------
# in default official PHP Dockerfile, the command is like below
#   COPY apache2-foreground /usr/local/bin/
#   WORKDIR /var/www/html
#   EXPOSE 80
#   CMD ["apache2-foreground"]
# but instead of using that, we will use daemon initialization syntax by phusion/baseimage

RUN mkdir /etc/service/apache2
COPY apache2-foreground /etc/service/apache2/run
RUN chmod +x /etc/service/apache2/run

WORKDIR /var/www/html
EXPOSE 80

#-------------------------------------------------------------------------------

#-------------------------------------------------------------------------------
# [DOCUMENTATION]
#
# ----------------------------------------
# -- Adding additional daemons --
# Write shell script which named `run` inside directory `/etc/service/<SERVICE_NAME>`.
# Then make it executable.
# WARNING :
#   Note that the shell script must run the daemon without letting it daemonize/fork it.
#   Usually, daemons provide a command line flag or a config file option for that.
#
# Example file : memcached.sh
#   #!/bin/sh
#   #`/sbin/setuser memcache` runs the given command as the user `memcache`.
#   #If you omit that part, the command will be run as root.
#   exec /sbin/setuser memcache /usr/bin/memcached >>/var/log/memcached.log 2>&1
#
# Example Dockerfile commands :
#   RUN mkdir /etc/service/memcached
#   ADD memcached.sh /etc/service/memcached/run
#   RUN chmod +x /etc/service/memcached/run
#
# ----------------------------------------
# -- Running scripts during container startup --
# Write shell script which placed inside directory `/etc/my_init.d`.
# WARNING :
#   All scripts must exit correctly, e.g. with exit code 0. If any script exits with a non-zero exit code, the booting will fail.
#
# Example file : logtime.sh
#   #!/bin/sh
#   date > /tmp/boottime.txt
#
# Example Dockerfile commands :
#   RUN mkdir -p /etc/my_init.d
#   ADD logtime.sh /etc/my_init.d/logtime.sh
#   RUN chmod +x /etc/my_init.d/logtime.sh
#
# ----------------------------------------
# -- Centrally defining your own environment variables --
# All environment variables will be loaded by `/etc/my_init.d` from all files in directory `etc/container_environment`.
# To add environment variables, just add new file inside that directory with value.
#
# Example Dockerfile commands :
#   RUN echo Apachai Hopachai > /etc/container_environment/MY_NAME
# 
# Verify environment variables :
#   $ docker run -t -i <YOUR_NAME_IMAGE> /sbin/my_init -- bash -l
#   ...
#   *** Running bash -l...
#   $ echo $MY_NAME
#   Apachai Hopachai
#   $ ls /etc/container_environment
#   FOO  HELLO  HOME  HOSTNAME  MY_NAME  PATH  TERM  container
#
# ----------------------------------------
# -- Upgrading the operating system inside the container --
# Just execute upgrade command inside Dockerfile.
#
# Example Dockerfile commands :
#   RUN apt-get update && apt-get upgrade -y -o Dpkg::Options::="--force-confold"
#
# ----------------------------------------
# -- Login to the container, or running a command inside it, via SSH --
# `phusion/baseimage` already provide ssh service, but disable it by default.
# To enable it, just add your ssh key in Dockerfile.
#
# Example Dockerfile commands :
#   RUN rm -f /etc/service/sshd/down
#   ADD ssh/your_key.pub /tmp/your_key.pub
#   RUN cat /tmp/your_key.pub >> /root/.ssh/authorized_keys && rm -f /tmp/your_key.pub
#
# To connect into the docker container, just rebuild image which already contain ssh key. Then use ssh private key to login.
# Example :
#   -- Build the image
#   $ docker build -t <IMAGE_NAME> .
#   -- Get container ID
#   $ docker ps
#   -- Look for container IP address
#   $ docker inspect -f "{{ .NetworkSettings.IPAddress }}" <ID>
#   -- Login to the container
#   $ ssh -i /path-to/your_key -p <Port> root@<IP address>
#   -- Running a command inside the container
#   $ ssh -i /path-to/your_key -p <Port> root@<IP address> echo hello world
#-------------------------------------------------------------------------------

# Clean up APT when done.
#RUN apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*