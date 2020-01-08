FROM alpine:3.6

ENV TOR_VERSION 0.4.0.5

RUN addgroup -S tor \
    && adduser -D -S -h /var/lib/tor -s /sbin/nologin -G tor tor \
    && apk --no-cache add --virtual .build-deps \
        curl \
        build-base \
        libevent-dev \
        openssl-dev \
        zlib-dev \
    && curl https://dist.torproject.org/tor-$TOR_VERSION.tar.gz >tor.tar.gz \
    && mkdir -p /usr/src \
    && tar xvf tor.tar.gz -C /usr/src \
    && rm -f tor.tar.gz \
    && cd /usr/src/tor-$TOR_VERSION \
    && ./configure \
    && make -j$(getconf _NPROCESSORS_ONLN) \
    && make install \
    && cd / \
    && rm -rf /usr/src/tor-$TOR_VERSION \
    && rm -rf /usr/local/etc/ \
    && rm -rf /usr/local/share/doc/ /usr/local/share/man/ \
    && strip /usr/local/bin/tor /usr/local/bin/tor-gencert /usr/local/bin/tor-resolve \
    && apk del .build-deps \
    \
    && runDeps="$( \
        scanelf --needed --nobanner --format '%n#p' /usr/local/bin/* \
            | tr ',' '\n' \
            | sort -u \
            | awk 'system("[ x`find /usr/local/lib/ -name " $1 "` = x ]") == 0 { print "so:" $1 } { next }' \
    )" \
    && apk --no-cache add --virtual .tor-rundeps $runDeps \
    && mkdir -p /etc/tor

COPY torrc /etc/tor/torrc

EXPOSE 9050

USER tor

CMD ["tor", "-f", "/etc/tor/torrc"]
