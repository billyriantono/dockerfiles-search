# Shadowsocks Server Dockerfile

FROM alpine

ARG SS_VER=3.2.5
ARG SS_DOWNLOAD=https://github.com/shadowsocks/shadowsocks-libev/releases/download/v${SS_VER}/shadowsocks-libev-${SS_VER}.tar.gz
ARG OBFS_DOWNLOAD=https://github.com/shadowsocks/simple-obfs.git

RUN set -ex && apk upgrade \
    && apk add bash tzdata rng-tools \
    && apk add --no-cache --virtual .build-deps \
        gcc \ 
        make \
        openssl \
        libpcre32 \
        g++ \
        curl \
        autoconf \
        build-base \
        libtool \
        linux-headers \
        libressl-dev \
        zlib-dev \
        asciidoc \
        udns-dev \
        xmlto \
        pcre-dev \
        automake \
        mbedtls-dev \
        libsodium-dev \
        c-ares-dev \
        libev-dev \
        tar \
        git \
    && curl -fsSL ${SS_DOWNLOAD} | tar xz \
    && (cd shadowsocks-libev-${SS_VER} \
    && ./configure --prefix=/usr --disable-documentation \
    && make install) \
    && git clone ${OBFS_DOWNLOAD} \
    && (cd simple-obfs \
    && git submodule update --init --recursive \
    && ./autogen.sh && ./configure --prefix=/usr --disable-documentation\
    && make && make install) \
    && cd .. \
    && runDeps="$( \
        scanelf --needed --nobanner /usr/bin/ss-* /usr/local/bin/obfs-* \
        | awk '{ gsub(/,/, "\nso:", $2); print "so:" $2 }' \
        | xargs -r apk info --installed \
        | sort -u \
        )" \
    && apk add --virtual .run-deps $runDeps \
    && apk del .build-deps \
    && rm -rf shadowsocks-libev-${SS_VER}.tar.gz \
        shadowsocks-libev-${SS_VER} \
        simple-obfs \
        /var/cache/apk/*

ENV SS_PORT=8388 
ENV PASSWORD=value 
ENV SS_METHOD=chacha20-ietf-poly1305 
ENV SS_TIMEOUT=60 
ENV DNS_ADDR=8.8.8.8,8.8.4.4 
ENV PLUGIN=obfs-server 
ENV PLUGIN_OPTS obfs=tls;fast-open;failover=0.0.0.0:8443

EXPOSE $SS_PORT/tcp $SS_PORT/udp

ENTRYPOINT ss-server -p $SS_PORT -k $PASSWORD -m $SS_METHOD -t $SS_TIMEOUT -d $DNS_ADDR --plugin $PLUGIN --plugin-opts $PLUGIN_OPTS -u --fast-open --no-delay

