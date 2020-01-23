FROM alpine:3.7

RUN apk add --no-cache \
    autoconf \
    bash \
    bzip2-dev \
    ca-certificates \
    coreutils \
    curl \
    curl-dev \
    dpkg-dev dpkg \
    file \
    g++ \
    gcc \
    git \
    gnupg \
    icu-dev \
    libc-dev \
    libedit-dev \
    libevent-dev \
    libjpeg-turbo-dev \
    libmcrypt-dev \
    libpng-dev \
    libxml2-dev \
    libxslt-dev \
    m4 \
    make \
    openssl-dev \
    pkgconf \
    re2c \
    readline-dev \
    sqlite-dev \
    tar \
    tidyhtml-dev \
    tidyhtml-libs \
    xz \
# https://github.com/docker-library/php/issues/494
    openssl

RUN set -x \
    && curl http://www.sqlite.org/src/raw/tool/lemon.c?name=7f7735326ca9c3b48327b241063cee52d35d44e20ebe1b3624a81658052a4d39 -o lemon.c \
    && gcc -o lemon lemon.c \
    && mv lemon /usr/local/bin/ \
    && rm -f lemon.c

ENV PHPENV_ROOT /opt/phpenv
ENV PATH "${PHPENV_ROOT}/bin:${PHPENV_ROOT}/shims:$PATH"

RUN set -x \
    && phpenv_version=085261129f7231fcd3b34401ad4af84b21df62eb \
    && php_build_version=8b5f7afa828709c115c49c0f864dad598cb4fc1f \
    && git clone https://github.com/madumlao/phpenv.git ${PHPENV_ROOT} \
    && (cd ${PHPENV_ROOT} && git checkout ${phpenv_version}) \
    && git clone https://github.com/php-build/php-build $(phpenv root)/plugins/php-build \
    && phpenv rehash
