FROM debian:stretch-slim

RUN set -eux; \
    { \
        echo 'Package: php*'; \
        echo 'Pin: release *'; \
        echo 'Pin-Priority: -1'; \
    } > /etc/apt/preferences.d/no-debian-php

RUN apt-get update && apt-get install -y \
    autoconf zip unzip dpkg-dev file g++ gcc libc-dev \
    make pkg-config bison re2c ca-certificates curl xz-utils \
    --no-install-recommends && rm -r /var/lib/apt/lists/*

ENV PHP_INI_DIR /usr/local/etc/php
RUN mkdir -p $PHP_INI_DIR/conf.d

ENV PHP_CFLAGS="-fstack-protector-strong -fpic -fpie -O2"
ENV PHP_CPPFLAGS="$PHP_CFLAGS"
ENV PHP_LDFLAGS="-Wl,-O1 -Wl,--hash-style=both -pie"

RUN apt-get update; \
    apt-get install -y --no-install-recommends wget dirmngr; \
    rm -rf /var/lib/apt/lists/*; \
    mkdir -p /usr/src; \
    cd /usr/src; \
    wget -O php.zip https://codeload.github.com/php/php-src/zip/PHP-7.4; \
    apt-get purge -y --auto-remove -o APT::AutoRemove::RecommendsImportant=false wget dirmngr;

RUN set -eux; \
    \
    savedAptMark="$(apt-mark showmanual)"; \
    apt-get update; \
    apt-get install -y --no-install-recommends \
        libcurl4-openssl-dev libedit-dev libsodium-dev libsqlite3-dev libffi-dev libpng-dev \
        libssl-dev libxml2-dev zlib1g-dev libonig-dev libbz2-dev libenchant-dev  libgmp-dev \
	libc-client-dev  libkrb5-dev firebird-dev libldb-dev libldap2-dev unixodbc-dev \
    ; \
    sed -e 's/stretch/buster/g' /etc/apt/sources.list > /etc/apt/sources.list.d/buster.list; \
    { \
        echo 'Package: *'; \
        echo 'Pin: release n=buster'; \
        echo 'Pin-Priority: -10'; \
        echo; \
        echo 'Package: libargon2*'; \
        echo 'Pin: release n=buster'; \
        echo 'Pin-Priority: 990'; \
    } > /etc/apt/preferences.d/argon2-buster; \
    apt-get update; \
    apt-get install -y --no-install-recommends libargon2-dev; \
    rm -rf /var/lib/apt/lists/*; \
    \
    export \
        CFLAGS="$PHP_CFLAGS" \
        CPPFLAGS="$PHP_CPPFLAGS" \
        LDFLAGS="$PHP_LDFLAGS" \
    ; \
    mkdir -p /usr/src/php/; \
    unzip /usr/src/php.zip -d /usr/src/php; \
    cd /usr/src/php/php-src-*; \
    gnuArch="$(dpkg-architecture --query DEB_BUILD_GNU_TYPE)"; \
    debMultiarch="$(dpkg-architecture --query DEB_BUILD_MULTIARCH)"; \
    if [ ! -d /usr/include/curl ]; then \
        ln -sT "/usr/include/$debMultiarch/curl" /usr/local/include/curl; \
    fi; \
    ./buildconf; \
    ./configure \
        --build="$gnuArch" \
        --enable-bcmath \
        --enable-dom \
        --enable-filter \
	--enable-intl \
        --enable-json \
        --enable-libxml \
        --enable-mbstring \
        --enable-pdo \
        --enable-pdo_mysql \
        --enable-phar \
	--enable-redis \
        --enable-simplexml \
	--enable-soap \
        --enable-sockets \
        --enable-tokenizer \
        --enable-xml \
        --enable-xmlreader \
        --enable-xmlwriter \
        --with-zlib \
        --with-config-file-path="$PHP_INI_DIR" \
        --with-config-file-scan-dir="$PHP_INI_DIR/conf.d" \
        --with-openssl \
        --with-sodium=shared \
        \
        $(test "$gnuArch" = 's390x-linux-gnu' && echo '--without-pcre-jit') \
        --with-libdir="lib/$debMultiarch" \
    ; \
    make -j "$(nproc)"; \
    make install; \
    find /usr/local/bin /usr/local/sbin -type f -executable -exec strip --strip-all '{}' + || true; \
    make clean; \
    \
    cp -v php.ini-* "$PHP_INI_DIR/"; \
    \
    cd /; \
    rm -rf /usr/src/php; \
    \
    apt-mark auto '.*' > /dev/null; \
    [ -z "$savedAptMark" ] || apt-mark manual $savedAptMark; \
    find /usr/local -type f -executable -exec ldd '{}' ';' \
        | awk '/=>/ { print $(NF-1) }' \
        | sort -u \
        | xargs -r dpkg-query --search \
        | cut -d: -f1 \
        | sort -u \
        | xargs -r apt-mark manual \
    ; \
    apt-get purge -y --auto-remove -o APT::AutoRemove::RecommendsImportant=false; \
    \
    php --version

CMD ["php", "--version"]
