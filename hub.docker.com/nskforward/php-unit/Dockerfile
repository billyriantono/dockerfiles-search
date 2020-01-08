FROM alpine:3.9

ENV PHP_VERSION 7.3.3
ENV REDIS_VERSION 4.2.0
ENV UNIT_VERSION 1.8.0
ENV PHP_BUILD_DEPS "dpkg-dev dpkg pkgconf gcc g++ libc-dev libc-dev make autoconf make file bison re2c tar wget"
ENV PHP_INI_DIR "/usr/local/etc/php"

RUN set -x \
    && apk add --no-cache ca-certificates postgresql-dev libsodium-dev argon2-dev \
    && apk add --no-cache --virtual .build-deps $PHP_BUILD_DEPS \
    \
    && mkdir -p $PHP_INI_DIR/conf.d \
    && wget -nv -O /tmp/php.tar.gz "https://secure.php.net/get/php-$PHP_VERSION.tar.gz/from/this/mirror" \
    && cd /tmp \
    && tar -xf php.tar.gz \
    && cd /tmp/php-$PHP_VERSION \
    && ./configure \
        --with-config-file-path="$PHP_INI_DIR" \
        --with-config-file-scan-dir="$PHP_INI_DIR/conf.d" \
        --disable-all \
        --enable-option-checking=fatal \
        --enable-opcache \
        --enable-pdo \
        --enable-filter \
        --enable-hash \
        --enable-json \
        --enable-ctype \
        --enable-embed \
        --with-pdo-pgsql \
        --without-sqlite3 \
        --without-pdo_sqlite \
        --without-pdo_sqlite \
        --without-iconv \
        --with-password-argon2 \
        --with-sodium \
        CFLAGS="-fstack-protector-strong -fpic -fpie -O2" \
    \
    && make -j "$(nproc)" \
    && make install \
    && make clean \
    \
    && wget -nv -O /tmp/redis.tar.gz "https://github.com/phpredis/phpredis/archive/$REDIS_VERSION.tar.gz" \
    && cd /tmp \
    && tar -xf redis.tar.gz \
    && cd /tmp/phpredis-$REDIS_VERSION \
    && phpize \
    && ./configure --disable-redis-session \
    && make \
    && make install \
    && make clean \
    && echo "extension=redis.so" > /usr/local/etc/php/conf.d/redis.ini \
    && echo "zend_extension=opcache.so" > /usr/local/etc/php/conf.d/opcache.ini \
    \
    && wget -nv -O /tmp/unit.tar.gz "https://unit.nginx.org/download/unit-$UNIT_VERSION.tar.gz" \
    && cd /tmp \
    && tar -xf unit.tar.gz \
    && cd /tmp/unit-$UNIT_VERSION \
    && mkdir -p /opt/unit/state -m 777 \
    && ./configure --prefix=/opt/unit --log=/dev/stdout \
    && ./configure php --module=php72 --config=/usr/local/bin/php-config --lib-path=/usr/local/lib \
    && make all \
    && make install \
    && make test \
    && make clean \
    \
    && apk del .build-deps \
    && rm -rf /var/cache/apk/* \
    && rm -rf /tmp/*

COPY index.php /app/index.php
COPY php.ini $PHP_INI_DIR/php.ini
COPY config.json /opt/unit/state/conf.json

EXPOSE 80
ENTRYPOINT ["/opt/unit/sbin/unitd"]
CMD ["--no-daemon", "--control", "unix:/opt/unit/control.unit.sock"]
