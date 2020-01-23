FROM alpine:latest

ENV VERSION 4.1.5
LABEL maintainer="support@opensvc.com"

RUN \
	apk --update add --no-cache musl bash libstdc++ file openssl && \
	apk add --no-cache --virtual .build-deps curl build-base wget boost-dev \
                autoconf automake bison flex g++ libtool make ragel \
		boost-program_options boost-serialization openssl-dev && \
	curl -sS https://downloads.powerdns.com/releases/pdns-$VERSION.tar.bz2 | \
	tar xjf - -C . && \
	cd pdns-* && \
	./configure --with-modules="remote" --without-lua && \
	make && \
	make install && \
	cd .. && rm -fr pdns-* && \
	apk del curl build-base wget boost-dev autoconf automake bison \
		flex g++ libtool make ragel openssl-dev && \
	apk del .build-deps

EXPOSE 5553/udp 5553/tcp

ENTRYPOINT ["/usr/local/sbin/pdns_server"]
