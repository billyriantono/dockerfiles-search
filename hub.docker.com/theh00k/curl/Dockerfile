FROM alpine:3.8

RUN apk add --no-cache --virtual .build-deps autoconf automake libtool cmake git make g++ linux-headers && \
  mkdir /tmp/build && cd /tmp/build && \
  git clone git://git.openssl.org/openssl.git && \
  cd openssl \
  export KERNEL_BITS=64 && \
  ./Configure linux-generic64 && \
  ./config shared enable-ec_nistp_64_gcc_128 --openssldir=/usr/local/openssl --prefix=/usr/local/openssl && \
  make && make install && \
  rm -rf /tmp/build && \
  mkdir /tmp/build && cd /tmp/build && \
  git clone https://github.com/google/brotli && \
  cd brotli && \
  mkdir out && cd out && \
  ../configure-cmake && \
  make && make test && make install && \
  rm -rf /tmp/build && \
  mkdir /tmp/build && cd /tmp/build && \
  git clone https://github.com/tatsuhiro-t/nghttp2 && \
  cd nghttp2 && \
  autoreconf -i && automake && autoconf && \
  ./configure && \
  make && make install && \
  rm -rf /tmp/build && \
  mkdir /tmp/build && cd /tmp/build && \
  git clone https://github.com/curl/curl && \
  cd curl && \
  ./buildconf && \
  ./configure --with-nghttp2=/usr/local --with-ssl=/usr/local/openssl --disable-shared --with-brotli && \
  make && make install && \
  rm -rf /tmp/build && \
  apk del .build-deps && \
  apk add ca-certificates

ENV LD_LIBRARY_PATH=/usr/local/openssl/lib

ENTRYPOINT ["curl"]
