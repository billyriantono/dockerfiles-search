# File: Dockerfile
#
# Author: Massimo Cannavo <massimo5cannavo@gmail.com>
# Date:   Sun Jul 29 11:59:10 PDT 2018
#
# Dockerfile that builds curl.
#
# Usage: docker container run --rm --name curl \
#          massimocannavo/curl http://example.com

FROM alpine:3.8 as build

ENV MBED_TLS_VER 2.12.0
ENV CURL_VER 7.61.1

RUN apk add --no-cache \
  g++ \
  make \
  nghttp2-dev \
  nghttp2-libs \
  perl \
  \
  && addgroup curl && adduser -D -s /bin/sh -G curl curl \
  \
  && mkdir --parents /usr/local/etc \
  \
  && grep curl /etc/group > /usr/local/etc/group \
  && grep curl /etc/passwd > /usr/local/etc/passwd \
  \
  && wget --directory-prefix=/usr/local/etc \
    https://curl.haxx.se/ca/cacert.pem \
  \
  && wget "https://tls.mbed.org/download/mbedtls-${MBED_TLS_VER}-apache.tgz" \
  && tar --extract --gzip --verbose --file "mbedtls-${MBED_TLS_VER}-apache.tgz" \
  && cd "mbedtls-${MBED_TLS_VER}" \
  \
  make && make install \
  \
  && wget "https://curl.haxx.se/download/curl-${CURL_VER}.tar.gz" \
  && tar --extract --gzip --verbose --file "curl-${CURL_VER}.tar.gz" \
  && cd "curl-${CURL_VER}" \
  \
  && ./configure \
    --enable-optimize \
    --with-nghttp2=/usr \
    --without-ssl \
    --with-mbedtls \
    --enable-ipv6 \
    --enable-unix-sockets \
    --without-libidn \
    --disable-static \
    --disable-ldap \
    --disable-manual \
    --disable-versioned-symbols \
    --enable-hidden-symbols \
  \
  && make && make install \
  \
  && strip --strip-all /usr/local/bin/curl \
  && strip --strip-all /usr/local/lib/libcurl.so.4

FROM scratch

COPY --from=build /lib/ld-musl-x86_64.so.1 /lib/
COPY --from=build /usr/lib/libnghttp2.so.14 /usr/lib/
COPY --from=build /lib/libz.so.1 /lib

COPY --from=build /usr/local/lib/libcurl.so.4 /usr/local/lib/
COPY --from=build /usr/local/bin/curl /usr/local/bin/

COPY --from=build /usr/local/etc/passwd /etc/passwd
COPY --from=build /usr/local/etc/group /etc/group
COPY --from=build /usr/local/etc/cacert.pem /etc/ssl/cert.pem

COPY --from=build /home/curl /home/curl

USER curl
WORKDIR /home/curl

ENTRYPOINT ["/usr/local/bin/curl"]
CMD ["-h"]
