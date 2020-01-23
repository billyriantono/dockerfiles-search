FROM alpine:latest
MAINTAINER ysslang <ysslang@qq.com>
ARG SS_VER=3.2.3
ARG SS_URL=https://github.com/shadowsocks/shadowsocks-libev/releases/download/v$SS_VER/shadowsocks-libev-$SS_VER.tar.gz
RUN set -ex \
        && apk add --no-cache \
        tzdata \
        net-tools \
        nodejs-npm \
        py2-pip \
        && apk add --no-cache --virtual .build-deps \
        autoconf \
        build-base \
        curl \
        libev-dev \
        linux-headers \
        libsodium-dev \
        mbedtls-dev \
        pcre-dev \
        sudo \
        tar \
        git \
        file \
        c-ares-dev \
        && cd /tmp \
        && curl -sSL $SS_URL | tar xz --strip 1 \
        && ./configure --prefix=/usr --disable-documentation \
        && make install \
        && cd .. \
        && runDeps="$( \
        scanelf --needed --nobanner /usr/bin/ss* \
        | awk '{ gsub(/,/, "\nso:", $2); print "so:" $2 }' \
        | xargs -r apk info --installed \
        | sort -u \
        )" \
        && apk add --no-cache --virtual .run-deps $runDeps \
        && pip install git+https://github.com/shadowsocks/shadowsocks.git@master \
        && npm i -g --unsafe-perm shadowsocks-manager \
        && apk del .build-deps \
        && export TZ='Asia/Shanghai'\
        && rm -rf /tmp/* /root/.cache/* /root.npm_cacache/*
ENTRYPOINT ["/usr/bin/ssmgr"]
