FROM alpine:latest

ENV BITCOIN_VERSION=0.15.0.1-r4
ENV BITCOIN_DATA=/var/lib/bitcoin

RUN addgroup -S bitcoin && adduser -S -g bitcoin bitcoin -h ${BITCOIN_DATA} && \
    apk add --update && \
    apk add --no-cache \
        libressl \
        libressl2.6-libcrypto \
        --repository http://dl-cdn.alpinelinux.org/alpine/edge/main && \
    apk add --no-cache \ 
        bitcoin=${BITCOIN_VERSION} \
        bitcoin-cli=${BITCOIN_VERSION} \
        bitcoin-tx=${BITCOIN_VERSION} \
        --repository http://dl-cdn.alpinelinux.org/alpine/edge/community && \
    apk add sudo && \
    rm -rf /var/cache/apk/* && \
    chmod 644 /etc/bitcoin.conf && \
    mkdir -p ${BITCOIN_DATA} && \
    chown -R bitcoin:bitcoin ${BITCOIN_DATA} && \
    chmod 700 ${BITCOIN_DATA}
    
WORKDIR ${BITCOIN_DATA}

USER bitcoin

VOLUME [ "/var/lib/bitcoin" ]

EXPOSE 8333

ENTRYPOINT ["bitcoind"]

CMD ["-printtoconsole"]