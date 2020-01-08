FROM alpine:3.4

LABEL maintainer="Jamie Isaacs <pdt256@gmail.com>"

WORKDIR /usr/local/src

ENV PHP_VERSION=7.1.8
ENV PHP_URL="https://secure.php.net/get/php-$PHP_VERSION.tar.gz/from/this/mirror" \
    PHP_MD5="dc3fa0355ff74f61f110beb892ec6f5e" \
    PHP_CFLAGS="-fstack-protector-strong -fpic -fpie -O2" \
    PHP_CPPFLAGS="$PHP_CFLAGS" \
    PHP_LDFLAGS="-Wl,-O1 -Wl,--hash-style=both -pie" \
    PHP_EXTRA_CONFIGURE_ARGS="--enable-fpm --with-fpm-user=www-data --with-fpm-group=www-data" \
    PHP_INI_DIR="/usr/local/etc/php" \
    BUILD_DEPENDENCIES="\
        g++ \
        libc-dev \
        re2c \
        gettext-dev \
        coreutils \
        gcc \
        make \
        wget \
        curl-dev \
        libxml2-dev \
        jpeg-dev \
        libpng-dev \
        libedit-dev \
        openssl-dev \
        freetype-dev"

RUN apk upgrade --no-cache \
    && apk add --no-cache --virtual .build-deps $BUILD_DEPENDENCIES \
    && apk --update add tar \
    && wget -q $PHP_URL -O php.tgz \
    && set -xe; \
    \
    if [ -n "$PHP_MD5" ]; then \
        echo "$PHP_MD5 *php.tgz" | md5sum -c -; \
    fi; \
    \
    export CFLAGS="$PHP_CFLAGS" \
        CPPFLAGS="$PHP_CPPFLAGS" \
        LDFLAGS="$PHP_LDFLAGS" \
    && mkdir -p $PHP_INI_DIR/conf.d \
    && mkdir -p /usr/local/src/php \
    && tar zxf php.tgz -C /usr/local/src/php --strip-components=1 \
    && ( \
        cd /usr/local/src/php \
        && ./configure \
            --with-config-file-path="$PHP_INI_DIR" \
            --with-config-file-scan-dir="$PHP_INI_DIR/conf.d" \
            --disable-cgi \
            --disable-rpath \
            --enable-mbstring \
            --enable-mysqlnd \
            --enable-zip \
            --enable-exif \
            --with-curl \
            --with-gettext \
            --with-libedit \
            --with-openssl \
            --with-zlib \
            --with-gd \
            --with-jpeg-dir \
            --with-pdo-mysql=mysqlnd \
            --with-png-dir \
            --with-freetype-dir \
            $PHP_EXTRA_CONFIGURE_ARGS \
        && make -j "$(nproc)" \
        && make install \
    	&& { find /usr/local/bin /usr/local/sbin -type f -perm +0111 -exec strip --strip-all '{}' + || true; } \
        && make clean \
    ) \
    && rm /usr/local/src/php.tgz \
    && rm -rf /usr/local/src/php \
    && runDeps="$( \
		scanelf --needed --nobanner --format '%n#p' --recursive /usr/local \
			| tr ',' '\n' \
			| sort -u \
			| awk 'system("[ -e /usr/local/lib/" $1 " ]") == 0 { next } { print "so:" $1 }' \
	)" \
	&& apk add --no-cache --virtual .php-rundeps $runDeps \
    && apk del .build-deps \
	&& addgroup -g 82 -S www-data \
	&& adduser -u 82 -D -S -G www-data www-data \
    && mkdir -p /var/log/php-fpm \
    && chown www-data.www-data /var/log/php-fpm

COPY ./php-fpm.conf /usr/local/etc/php-fpm.conf
COPY ./php-fpm.d/ /usr/local/etc/php-fpm.d

EXPOSE 9000
CMD ["php-fpm"]
USER www-data
