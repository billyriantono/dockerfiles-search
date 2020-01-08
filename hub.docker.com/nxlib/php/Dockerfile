FROM nxlib/php:latest

MAINTAINER Garming Lau <garming@msn.com>

#####################################
# dependence lib:
#####################################
ENV PHPIZE_DEPS \
        autoconf \
        dpkg-dev dpkg \
        file \
        g++ \
        gcc \
        libc-dev \
        make \
        pkgconf \
        re2c \
        git \
        libev-dev \
        libevent-dev \
        jansson-dev \
        jemalloc-dev \
        openssl-dev \
        libtool 

ARG INSTALL_SWOOLE=true
#####################################
# swoole 4.x
#####################################
RUN set -xe && apk add --no-cache --virtual .swoole-persistent-deps hiredis-dev
RUN set -xe && apk add --no-cache --virtual .build-deps $PHPIZE_DEPS && \
cd /tmp && \
git clone https://github.com/swoole/swoole-src.git swoole && \
( \
    cd swoole && \
    git checkout v4.0.0 && \
    phpize && \
    ./configure --enable-openssl --enable-sockets --enable-async-redis --enable-mysqlnd && \
    make && \
    make install \
) && \
cd / && \
rm -rf /tmp/* && \
docker-php-ext-enable swoole && \
apk del .build-deps

WORKDIR /var/www

CMD ["php-fpm"]

EXPOSE 9000