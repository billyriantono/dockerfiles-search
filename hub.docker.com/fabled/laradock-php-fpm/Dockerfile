#
#--------------------------------------------------------------------------
# Image Setup
#--------------------------------------------------------------------------
#

FROM laradock/php-fpm:7.0--1.2

MAINTAINER fabled <fabled.vip@gmail.com>

ENV PHP_INI_DIR /usr/local/etc/php
ENV PHP_EXTRA_CONFIGURE_ARGS --enable-fpm --with-fpm-user=www-data --with-fpm-group=www-data --with-sqlite3=shared --with-pdo-sqlite=shared

RUN set -xe \
  && buildDeps=" \
    $PHP_EXTRA_BUILD_DEPS \
    libcurl4-openssl-dev \
    libedit-dev \
    libsqlite3-dev \
    libssl-dev \
    libxml2-dev \
  " \
  && apt-get update && apt-get install -y $buildDeps --no-install-recommends && rm -rf /var/lib/apt/lists/* \
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
  && make -j "$(nproc)" \
  && make install \
  && { find /usr/local/bin /usr/local/sbin -type f -executable -exec strip --strip-all '{}' + || true; } \
  && make clean \
  && docker-php-source delete \
  \
  && apt-get purge -y --auto-remove -o APT::AutoRemove::RecommendsImportant=false $buildDeps

EXPOSE 9000
CMD ["php-fpm"]
