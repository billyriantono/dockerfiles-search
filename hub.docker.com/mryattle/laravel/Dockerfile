FROM alpine:3.10 as building

RUN apk add --no-cache \
    php7-dev libmcrypt-dev build-base \
    php7-json php7-openssl php7-phar \
    php7-iconv php7-bcmath php7-mbstring \
    php7-dom php7-xml php7-xmlwriter php7-pdo \
    php7-tokenizer \
    unzip libaio libnsl musl-dev libstdc++


RUN mkdir mkdir -p /tmp/php7fpm
WORKDIR /tmp/php7fpm
RUN apk add --no-cache build-base

ADD docker/mcrypt-1.0.1.tgz .
RUN cd mcrypt-1.0.1 && \
    /usr/bin/phpize7 && \
    ./configure && make && make install
# /usr/local/lib/php/extensions/no-debug-non-zts-20180731/mcrypt.so

# OCI8 
# Oracle
ENV ORACLE_BASE /usr/lib/instantclient_12_1
ENV LD_LIBRARY_PATH /usr/lib/instantclient_12_1
ENV TNS_ADMIN /usr/lib/instantclient_12_1
ENV ORACLE_HOME /usr/lib/instantclient_12_1
ADD docker/instantclient-basic-linux.x64-12.1.0.2.0.zip /tmp/instantclient-basic-linux.x64-12.1.0.2.0.zip
ADD docker/instantclient-sdk-linux.x64-12.1.0.2.0.zip /tmp/instantclient-sdk-linux.x64-12.1.0.2.0.zip
RUN unzip -d /usr/lib/ /tmp/instantclient-basic-linux.x64-12.1.0.2.0.zip
RUN unzip -d /usr/lib/ /tmp/instantclient-sdk-linux.x64-12.1.0.2.0.zip
RUN rm /tmp/instantclient-basic-linux.x64-12.1.0.2.0.zip /tmp/instantclient-sdk-linux.x64-12.1.0.2.0.zip
RUN ln /usr/lib/instantclient_12_1/libclntsh.so.12.1 /usr/lib/libclntsh.so && \
    ln /usr/lib/instantclient_12_1/libocci.so.12.1 /usr/lib/libocci.so && \
    ln /usr/lib/instantclient_12_1/libociei.so /usr/lib/libociei.so && \
    ln /usr/lib/instantclient_12_1/libnnz12.so /usr/lib/libnnz12.so && \
    ln /usr/lib/libnsl.so.2.0.0  /usr/lib/libnsl.so.1 && \
    ln -s /usr/lib/instantclient_12_1/libclntsh.so.12.1 /usr/lib/instantclient_12_1/libclntsh.so && \
    ln -s /lib/libc.musl-x86_64.so.1 /lib/ld-linux-x86-64.so.2

ADD docker/php-7.3.11.tar.gz .
RUN cd php-7.3.11/ext/oci8; \
    /usr/bin/phpize7 && \
    ./configure --with-oci8=instantclient,/usr/lib/instantclient_12_1 --with-php-config=/usr/bin/php-config7 && \
    make && make install

# /usr/lib/php7/modules/
# /usr/lib/instantclient_12_1/
# links

# Install composer
ADD docker/composer-setup.php .
RUN php composer-setup.php --install-dir=/usr/local/bin --filename=composer --quiet && \
    rm composer-setup.php

# User where to publish the application
RUN addgroup -S laravel && adduser --home /opt/laravel --gecos "Laravel web application" --shell /bin/sh --ingroup laravel --disabled-password laravel
RUN mkdir -p /run/php
RUN mkdir -p /var/log/laravel; chown -R laravel:laravel /var/log/laravel

USER laravel
WORKDIR /opt/laravel
RUN /usr/bin/php7 /usr/local/bin/composer create-project --prefer-dist laravel/laravel="5.8.*" public_html

WORKDIR /opt/laravel/public_html
RUN /usr/bin/php7 /usr/local/bin/composer require league/fractal="0.17.0"
RUN /usr/bin/php7 /usr/local/bin/composer require barryvdh/laravel-cors="0.11.3"
RUN /usr/bin/php7 /usr/local/bin/composer require owen-it/laravel-auditing="9.0"
RUN /usr/bin/php7 /usr/local/bin/composer require doctrine/dbal="2.4.2"
RUN /usr/bin/php7 /usr/local/bin/composer require servo/fluidxml="1.20.3"

USER root
RUN touch /etc/php7/conf.d/00_oci8.ini
RUN echo 'extension=oci8.so' >> /etc/php7/conf.d/00_oci8.ini
RUN apk add --no-cache php7-pdo

USER laravel
RUN /usr/bin/php7 /usr/local/bin/composer require yajra/laravel-oci8="^5.8"

FROM alpine:3.10
LABEL Maintainer="Mauro Fasolo <mr.yattle@gmail.com>" \
      Description="Lightweight container with Laravel 5.8 & PHP-FPM 7.3 based on Alpine Linux."

RUN apk add --no-cache \
    php7-fpm php7-session php7-json \
    php7-openssl php7-phar \
    php7-iconv php7-bcmath php7-mbstring \
    php7-dom php7-xml php7-xmlwriter php7-pdo \
    php7-tokenizer php7-intl php7-zip php7-pdo_pgsql \
    libmcrypt-dev libaio libnsl libstdc++

ENV ORACLE_BASE /usr/lib/instantclient_12_1
ENV LD_LIBRARY_PATH /usr/lib/instantclient_12_1
ENV TNS_ADMIN /usr/lib/instantclient_12_1
ENV ORACLE_HOME /usr/lib/instantclient_12_1

COPY --from=building /usr/lib/php7/modules/oci8.so /usr/lib/php7/modules/oci8.so
COPY --from=building /usr/lib/php7/modules/mcrypt.so /usr/lib/php7/modules/mcrypt.so
COPY --from=building /usr/local/bin/composer /usr/local/bin/composer
COPY --from=building /usr/lib/instantclient_12_1/libclntsh.so.12.1 /usr/lib/instantclient_12_1/libclntsh.so.12.1
COPY --from=building /usr/lib/instantclient_12_1/libclntshcore.so.12.1 /usr/lib/instantclient_12_1/libclntshcore.so.12.1
COPY --from=building /usr/lib/instantclient_12_1/libnnz12.so /usr/lib/instantclient_12_1/libnnz12.so
COPY --from=building /usr/lib/instantclient_12_1/libons.so /usr/lib/instantclient_12_1/libons.so 
COPY --from=building /usr/lib/instantclient_12_1/libmql1.so /usr/lib/instantclient_12_1/libmql1.so
COPY --from=building /usr/lib/instantclient_12_1/libipc1.so /usr/lib/instantclient_12_1/libipc1.so
#COPY --from=building /usr/lib/instantclient_12_1/libocci.so.12.1 /usr/lib/instantclient_12_1/libocci.so.12.1
COPY --from=building /usr/lib/instantclient_12_1/libociei.so /usr/lib/instantclient_12_1/libociei.so
COPY --from=building /opt/laravel/public_html /opt/laravel/public_html
ADD docker/laravel.conf /etc/php7/php-fpm.d/laravel.conf
RUN ln -s /lib/libc.musl-x86_64.so.1 /lib/ld-linux-x86-64.so.2 && \
    ln /usr/lib/instantclient_12_1/libnnz12.so /usr/lib/libnnz12.so && \
    ln /usr/lib/libnsl.so.2.0.0  /usr/lib/libnsl.so.1 && \
    touch /etc/php7/conf.d/00_oci8.ini; \
    echo 'extension=oci8.so' >> /etc/php7/conf.d/00_oci8.ini; \
    touch /etc/php7/conf.d/00_mcrypt.ini; \
    echo 'extension=mcrypt.so' >> /etc/php7/conf.d/00_mcrypt.ini && \
    addgroup -S laravel && adduser --home /opt/laravel --gecos "Laravel web application" --shell /bin/sh --ingroup laravel --disabled-password laravel && \
    mkdir -p /run/php; \
    mkdir -p /var/log/laravel; chown -R laravel:laravel /var/log/laravel; \
    chown -R laravel:laravel /opt/laravel/public_html; \
    mv /etc/php7/php-fpm.d/www.conf /etc/php7/php-fpm.d/www.conf.disabled

WORKDIR /opt/laravel/public_html
CMD /usr/sbin/php-fpm7 -F