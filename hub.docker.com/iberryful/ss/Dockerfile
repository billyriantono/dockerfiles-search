#
# Dockerfile for shadowsocks-libev
#

FROM alpine

ENV SERVER_ADDR 0.0.0.0
ENV SERVER_PORT 8388
ENV PASSWORD=
ENV METHOD      aes-256-gcm
ENV TIMEOUT     600
ENV DNS_ADDRS    8.8.8.8, 8.8.4.4

RUN set -ex && \
    apk add --no-cache --virtual .build-deps \
                                autoconf \
                                build-base \
                                libev-dev \
                                libtool \
                                linux-headers \
                                udns-dev \
                                libsodium-dev \
                                c-ares-dev \
                                mbedtls-dev \
                                pcre-dev \
                                tar \
                                git \
                                automake \
                                udns-dev && \
    cd /tmp && \
    git clone --depth=1 https://github.com/shadowsocks/simple-obfs.git . && \
    git submodule update --init --recursive && \
    ./autogen.sh && \
    ./configure --prefix=/usr --disable-documentation && make && \
    make install && \
    cd .. && \
    find /tmp -mindepth 1 -delete && \

    cd /tmp && \
    git clone --depth=1 https://github.com/shadowsocks/shadowsocks-libev.git . && \
    git submodule update --init --recursive && \
    ./autogen.sh && \
    ./configure --prefix=/usr --disable-documentation && make && \
    make install && \
    cd .. && \

    runDeps="$( \
        scanelf --needed --nobanner /usr/bin/ss-* \
            | awk '{ gsub(/,/, "\nso:", $2); print "so:" $2 }' \
            | xargs -r apk info --installed \
            | sort -u \
    )" && \
    apk add --no-cache --virtual .run-deps $runDeps && \
    apk del .build-deps && \
    rm -rf /tmp/*

USER nobody

CMD ss-server -s $SERVER_ADDR \
              -p $SERVER_PORT \
              -k $PASSWORD \
              -m $METHOD \
              -t $TIMEOUT \
              --fast-open \
              -d $DNS_ADDRS \
              -u \
              --plugin obfs-server --plugin-opts "obfs=tls;obfs-host=www.bing.com"
