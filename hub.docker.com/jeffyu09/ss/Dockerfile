# Dockerfile

FROM alpine

LABEL maintainer "XX@XX.com"

ENV TZ "Asia/Hong_Kong"

RUN set -ex \
    # Build environment setup
    # && adduser ssuser -D \
    && apk add --no-cache --virtual .build-deps \
        autoconf \
        automake \
        build-base \
        c-ares-dev \
        libev-dev \
        libtool \
        libsodium-dev \
        linux-headers \
        mbedtls-dev \
        pcre-dev \
        git \
        # git clone repo
        && cd /tmp \
        && git clone https://github.com/shadowsocks/shadowsocks-libev.git \
        # Build & install
        && cd /tmp/shadowsocks-libev \
        && git submodule update --init --recursive \
        && ./autogen.sh \
        && ./configure --prefix=/usr --disable-documentation \
        && make install \
        && apk del .build-deps \
        # Runtime dependencies setup
        && apk add --no-cache \
            rng-tools \
            $(scanelf --needed --nobanner /usr/bin/ss-* \
            | awk '{ gsub(/,/, "\nso:", $2); print "so:" $2 }' \
            | sort -u) \
    && rm -rf /tmp/shadowsocks-libev \
    && mkdir /etc/ss

# USER ssuser
USER root

ENTRYPOINT ["ss-manager", "-c", "/etc/ss/ss_libev_config.json"]