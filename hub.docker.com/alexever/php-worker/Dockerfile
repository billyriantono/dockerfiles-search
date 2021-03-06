FROM php:7.3-alpine

LABEL maintainer="Alex Chiang"

ENV SUPERVISOR_VER 4.0.2
ENV MYSQL_XDEVAPI_VER 8.0.16

# Add a non-root user:
ARG PUID=1000
ENV PUID ${PUID}
ARG PGID=1000
ENV PGID ${PGID}

RUN addgroup -g ${PGID} laradock \
    && adduser -D -G laradock -u ${PUID} laradock \
    && apk add --no-cache --update python3 python3-dev py-pip build-base autoconf curl protobuf protobuf-dev boost boost-dev \
    && pip3 install -U pip \
    && pip3 install supervisor \
    && mkdir -p /usr/src/temp \
    && cd /usr/src/temp \
    && curl -fSL https://pecl.php.net/get/mysql_xdevapi-$MYSQL_XDEVAPI_VER.tgz -o mysql_xdevapi-$MYSQL_XDEVAPI_VER.tgz \
    && tar xf mysql_xdevapi-$MYSQL_XDEVAPI_VER.tgz \
    && cd mysql_xdevapi-$MYSQL_XDEVAPI_VER \
    && phpize \
    && ./configure \
    && make \
    && make install \
    && curl -fSL https://curl.haxx.se/ca/cacert.pem -o /etc/cacert.pem \
    && echo "openssl.cafile=/etc/cacert.pem" > /usr/local/etc/php/conf.d/docker-php-openssl-cafile.ini \
    && docker-php-ext-install opcache pdo_mysql pcntl \
    && pecl install redis \
    && docker-php-ext-enable opcache pdo_mysql pcntl redis mysql_xdevapi \
    && apk del curl openssl tar xz-libs xz python3-dev py-pip build-base autoconf protobuf-dev boost-dev \
    && rm -rf /usr/src /tmp/pear ~/.pearrc /usr/src/temp

CMD ["/usr/bin/supervisord", "-n", "-c",  "/etc/supervisord.conf"]