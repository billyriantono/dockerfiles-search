FROM doridian/alpine-builder:latest as builder

RUN apk add --no-cache ldns-dev libevent-dev autoconf automake libtool bsd-compat-headers yaml-dev

WORKDIR /usr/src

RUN git clone https://github.com/Doridian/evldns && \
	cd evldns && \
	autoreconf --install && \
	./configure && \
	make

RUN git clone https://github.com/getdnsapi/getdns.git && \
	cd getdns && \
	git checkout master && git submodule update --init && libtoolize -ci && autoreconf -fi && mkdir build && \
	cd build && \
	../configure --without-libidn --without-libidn2 --enable-stub-only --with-stubby && make && make install

FROM doridian/alpine-minit:latest
MAINTAINER Doridian

RUN apk add --no-cache dnsmasq curl stunnel libevent ldns yaml

RUN mkdir -p /config
COPY --from=builder /usr/src/evldns/fixed /usr/local/sbin/zerodns
COPY --from=builder /usr/local/bin/stubby /usr/local/sbin/stubby
COPY --from=builder /usr/local/lib/ /usr/lib/
COPY root/ /
EXPOSE 53/udp 53/tcp 853/tcp
VOLUME /config

