FROM debian:wheezy-slim

ENV VERSION_PHP 5.2.16
ENV PHP_INI_DIR /etc/php

RUN mkdir -p $PHP_INI_DIR/conf.d

RUN apt-get update
RUN apt-get install -y  vim curl patch make wget gcc perl bzip2 autoconf pkg-config \
    apache2 apache2-threaded-dev libapache2-mod-php5 libxml2-dev libcurl4-openssl-dev libjpeg-dev \
    libmysqlclient-dev libpng12-dev libreadline6-dev libssl-dev

RUN apt-get autoremove --purge && apt-get clean

RUN a2enmod rewrite

COPY conf/apache2.conf /etc/apache2/apache2.conf
COPY conf/000-default.conf /etc/apache2/sites-enabled/000-default.conf

RUN ln -s /usr/lib/x86_64-linux-gnu/libjpeg.a /usr/lib/libjpeg.a && \
    ln -s /usr/lib/x86_64-linux-gnu/libjpeg.so /usr/lib/libjpeg.so && \
    ln -s /usr/lib/x86_64-linux-gnu/libpng.a /usr/lib/libpng.a && \
    ln -s /usr/lib/x86_64-linux-gnu/libpng.so /usr/lib/libpng.so && \
    ln -s /usr/lib/x86_64-linux-gnu/libmysqlclient.so /usr/lib/libmysqlclient.so && \
    ln -s /usr/lib/x86_64-linux-gnu/libmysqlclient.a /usr/lib/libmysqlclient.a

COPY sources/php-$VERSION_PHP.tar.gz /usr/src
COPY sources/php-$VERSION_PHP.patch /usr/src

RUN cd /usr/src && \
    tar -zxvf php-$VERSION_PHP.tar.gz && \
    rm php-$VERSION_PHP.tar.gz && \
    mv php-$VERSION_PHP php && \
    cd php && \
    cat /usr/src/php-$VERSION_PHP.patch | patch -p0 && \
    ./configure \
        --with-config-file-path="$PHP_INI_DIR" \
        --with-config-file-scan-dir="$PHP_INI_DIR/conf.d" \
        --with-fpm-conf="$PHP_INI_DIR/php-fpm.conf" \
        --without-iconv && \
    make && make install

RUN mkdir -p /usr/local/lib/php/extensions/no-debug-non-zts-20060613/
COPY conf/php.ini /etc/php/php.ini
COPY conf/php.ini /etc/php/php-fpm.conf

COPY scripts/php-ext-configure.sh /bin/php-ext-configure
COPY scripts/php-ext-install.sh /bin/php-ext-install
COPY scripts/install-extensions.sh /bin/install-extensions

RUN install-extensions

COPY conf/bashrc.conf /root/.bashrc

WORKDIR /var/www/html

COPY scripts/run-apache.sh /bin/run-apache
CMD ["run-apache"]
