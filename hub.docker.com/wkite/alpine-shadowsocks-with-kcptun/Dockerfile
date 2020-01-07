FROM alpine:latest

ENV SS_VER=3.3.3 KCP_VER=20191127
ARG SS_URL=https://github.com/shadowsocks/shadowsocks-libev/releases/download/v$SS_VER/shadowsocks-libev-$SS_VER.tar.gz
ARG KCP_URL=https://github.com/xtaci/kcptun/releases/download/v$KCP_VER/kcptun-linux-amd64-$KCP_VER.tar.gz

RUN set -ex \
#   && export http_proxy=http://192.168.8.1:1080/ \
#   && export https_proxy=https://192.168.8.1:1080/ \
    && mkdir -p /mktmp \
    && cd /mktmp \
    && apk add --no-cache --virtual .build-deps \
                                    autoconf \
                                    build-base \
                                    wget \
                                    libev-dev \
                                    libtool \
                                    linux-headers \
                                    udns-dev \
                                    libsodium-dev \
                                    mbedtls-dev \
                                    pcre-dev \
                                    tar \
                                    tzdata \
                                    udns-dev \
                                    c-ares-dev \
    && cp /usr/share/zoneinfo/Asia/Shanghai /etc/localtime \
    && wget -q --no-check-certificate $KCP_URL -O - | tar xz server_linux_amd64 \
    && mv server_linux_amd64 /usr/bin/ \
    && wget -q --no-check-certificate $SS_URL -O - | tar xz --strip 1 \
    && ./configure --prefix=/usr --disable-documentation \
    && make -j4 \
    && cp src/ss-server /usr/bin/ \
    && cd .. \
    && runDeps="$(scanelf --needed --nobanner /usr/bin/ss-* \
            | awk '{ gsub(/,/, "\nso:", $2); print "so:" $2 }' \
            | xargs -r apk info --installed \
            | sort -u)" \
    && apk add --no-cache --virtual .run-deps $runDeps \
    && apk del .build-deps \
#   && unset http_proxy \
#   && unset https_proxy \
    && rm -rf /mktmp

ENV SS_PORT=8388 \
SS_PASSWORD=123456789 \
SS_METHOD=aes-256-cfb \
SS_TIMEOUT=300 \
SS_USER=nobody \
SS_DNS1=8.8.8.8 \
SS_DNS2=8.8.4.4 \
SS_FASTOPEN=--fast-open \
SS_UDP=-u \
KCP_PORT=9443 \
KCP_MTU=1400 \
KCP_MODE=fast \
KCP_ENCRYPT=none \
KCP_PASSWORD=none-encrypt \
KCP_SNDWND=1024 \
KCP_RCVWND=512 \
KCP_DATASHARD=10 \
KCP_PARITYSHARD=0 \
KCP_SOCKBUF=16777216 \
KCP_NOCOMP=''
#KCP_NOCOMP=--nocomp

EXPOSE $SS_PORT/tcp $KCP_PORT/udp

CMD ss-server \
    -p $SS_PORT \
    -k $SS_PASSWORD \
    -m $SS_METHOD \
    -t $SS_TIMEOUT \
    -a $SS_USER \
    -d $SS_DNS1 \
    -d $SS_DNS2 \
    -f /tmp/ss.pid \
    $SS_FASTOPEN \
    $SS_UDP \
    && server_linux_amd64 \
    -l ":$KCP_PORT" \
    -t "127.0.0.1:$SS_PORT" \
    --mtu $KCP_MTU \
    --mode $KCP_MODE \
    --crypt $KCP_ENCRYPT \
    --key $KCP_PASSWORD \
    --sndwnd $KCP_SNDWND \
    --rcvwnd $KCP_RCVWND \
    --datashard $KCP_DATASHARD \
    --parityshard $KCP_PARITYSHARD \
    --sockbuf $KCP_SOCKBUF \
    $KCP_NOCOMP
