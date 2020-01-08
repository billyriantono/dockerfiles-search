FROM tomashavlas/httpd:2.4-debian9

USER 0

ENV PHP_VERSION=7.2 \
    PHP_RELEASE=7.2.7 \
    PHP_CHECKSUM=eb01c0153b3baf1f64b8b044013ce414b52fede222df3f509e8ff209478f31f0 \
    PHP_SOURCE=/usr/src/php \
    PHP_TARBALL=/usr/src/php-7.2.7.tar.xz

LABEL name="tomashavlas/php-httpd" \
      version="${PHP_VERSION}" \
      release="${PHP_RELEASE}" \
      maintaner="Tomáš Havlas <tomas@havlas.me>" \
      vendor="Tomáš Havlas" \
      io.openshift.s2i.scripts-url=image:///usr/lib/s2i

ENV PHP_CONF_PATH=/etc/php \
    PHP_CONFD_PATH=/etc/php/conf.d \
    PHP_LOCK_PATH=/var/lock/php

RUN apt-get update \
 && BUILD_DEPS=" \
        autoconf \
        ca-certificates \
        file \
        gcc \
        g++ \
        make \
        libapr1-dev \
        libaprutil1-dev \
        libargon2-0-dev \
        libcurl4-openssl-dev \
        libssl1.0-dev \
        libxml2-dev \
        pkg-config \
        zlib1g-dev " \
 && RUNTIME_DEPS=" \
        gettext-base \
        libargon2-0 \
        libcurl3 \
        libnss-wrapper \
        libssl1.0.2 \
        libxml2 \
        xz-utils \
        zlib1g " \
 && apt-get install --yes --no-install-recommends --verbose-versions ${BUILD_DEPS} ${RUNTIME_DEPS} \
 \
 && rm --recursive /var/lib/apt/lists/*

RUN apt-get update \
 && BUILD_DEPS=" \
        wget " \
 && apt-get install --yes --no-install-recommends --verbose-versions ${BUILD_DEPS} \
 \
 && wget -O "${PHP_TARBALL}" "https://secure.php.net/get/php-${PHP_RELEASE}.tar.xz/from/this/mirror" \
 && echo "${PHP_CHECKSUM} *${PHP_TARBALL}" | sha256sum --check - \
 \
 && apt-get purge --yes --auto-remove ${BUILD_DEPS} \
 && rm --recursive /var/lib/apt/lists/*

COPY [ "./root/usr/bin/docker-php-configure", "./root/usr/bin/docker-php-install", "./root/usr/bin/docker-php-source", "/usr/bin/" ]

RUN docker-php-source extract \
 && docker-php-install \
        --disable-cgi \
        --disable-simplexml \
        --disable-phpdbg \
        --enable-ftp \
        --enable-mbstring \
        --enable-mysqlnd \
        --with-curl \
        --with-openssl \
        --with-password-argon2 \
        --with-zlib \
        --without-iconv \
 && docker-php-source delete

ENV CONTAINER_PASSWD_PATH="${PHP_CONF_PATH}/passwd"

COPY [ "./s2i/bin", "${S2I_BIN_PATH}/" ]
COPY [ "./common/root", "./root", "./${PHP_VERSION}/root", "/" ]
RUN /usr/lib/container-entrypoint/php-setup \
 && /usr/lib/container-entrypoint/php-generate-conf_available_d

USER 48

CMD [ "/usr/lib/s2i/usage" ]
