FROM alpine:latest

ENV KCP_VER=20190409
ARG KCP_URL=https://github.com/xtaci/kcptun/releases/download/v$KCP_VER/kcptun-linux-amd64-$KCP_VER.tar.gz

RUN set -ex \
    && apk add --no-cache squid wget dumb-init \
    && wget -q --no-check-certificate $KCP_URL -O - | tar xz server_linux_amd64 \
    && mv server_linux_amd64 /usr/bin/

ENV KCP_PORT=29900 \
    KCP_MTU=1400 \
    KCP_MODE=fast \
    KCP_ENCRYPT=aes \
    KCP_PASSWORD=default-password \
    KCP_SNDWND=128 \
    KCP_RCVWND=512 \
    KCP_DATASHARD=10 \
    KCP_PARITYSHARD=3 \
    KCP_NOCOMP=''
    #KCP_NOCOMP=--nocomp

EXPOSE 3128/tcp $KCP_PORT/udp

ENTRYPOINT ["/usr/bin/dumb-init", "--"]

CMD squid \
    && server_linux_amd64 \
    -l ":$KCP_PORT" \
    -t "127.0.0.1:3128" \
    --mtu $KCP_MTU \
    --mode $KCP_MODE \
    --crypt $KCP_ENCRYPT \
    --key $KCP_PASSWORD \
    --sndwnd $KCP_SNDWND \
    --rcvwnd $KCP_RCVWND \
    --datashard $KCP_DATASHARD \
    --parityshard $KCP_PARITYSHARD \
    $KCP_NOCOMP
