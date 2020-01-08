FROM anapsix/alpine-java

MAINTAINER ss <shadowsocks@shadowsocks.org>

ARG SS_URL=https://github.com/shadowsocks/shadowsocks-libev.git

ENV XS_PORT 130
ENV SS_PORT 8388

ADD entrypoint /

RUN set -ex && \
    mkdir /xs && \
    chmod +x /entrypoint && \
    apk add openrc libpcap iptables --no-cache && \
    apk add --no-cache --virtual .build-deps \
                                asciidoc \
                                autoconf \
                                build-base \
                                git \
                                libtool \
                                linux-headers \
                                openssl-dev \
                                pcre-dev \
                                tar \
                                xmlto && \
    rm -rf /tmp && \
    git clone $SS_URL /tmp && \
    cd /tmp && \
    ./configure --prefix=/usr --disable-documentation && \
    make install && \
    cd /xs && \
    wget -O xsocks_server.zip http://www.tcpspeed.com/tcpspeed/tcpspeed_server.zip && \
	unzip xsocks_server.zip && rm -f xsocks_server.zip && \
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

USER root

EXPOSE $SS_PORT/tcp $SS_PORT/udp $XS_PORT/udp

ENTRYPOINT ["/entrypoint"]
CMD ["-h"]
