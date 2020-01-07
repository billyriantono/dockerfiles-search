FROM alpine:edge

RUN echo "@community http://dl-4.alpinelinux.org/alpine/edge/community" >> /etc/apk/repositories && \ 
    apk add --no-cache tor && \
    chown -R tor /etc/tor && \
    echo "SocksPort 0.0.0.0:9050" >> /etc/tor/torrc.sample && \
    mv /etc/tor/torrc.sample /etc/tor/torrc

EXPOSE 9050

USER tor

ENTRYPOINT [ "tor" ]

