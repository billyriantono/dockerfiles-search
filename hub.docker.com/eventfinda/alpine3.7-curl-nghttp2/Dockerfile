FROM alpine:3.7

LABEL maintainer="Eventfinda Developers <dev@eventfindahq.com>"

ARG CURL_VERSION=7.60.0

RUN apk add --no-cache openssl nghttp2 ca-certificates \
    && apk add --no-cache --virtual .curldeps g++ make perl openssl-dev nghttp2-dev \
    && wget https://curl.haxx.se/download/curl-$CURL_VERSION.tar.bz2 \
    && tar xjf curl-$CURL_VERSION.tar.bz2 \
    && rm curl-$CURL_VERSION.tar.bz2 \
    && cd curl-$CURL_VERSION \
    && ./configure \
        --with-nghttp2=/usr \
        --prefix=/usr \
        --with-ssl \
        --enable-ipv6 \
        --enable-unix-sockets \
        --without-libidn \
        --disable-static \
        --disable-ldap \
        --with-pic \
    && make \
    && make install \
    && cd / \
    && rm -r curl-$CURL_VERSION \
    && rm -r /var/cache/apk \
    && rm -r /usr/share/man \
    && apk del .curldeps

CMD ["curl", "--http2", "-I", "-s", "https://nghttp2.org"]