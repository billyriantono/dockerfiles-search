FROM alpine
MAINTAINER Roger Cui <itabas016@gmail.com>

COPY . /tmp/repo
RUN set -ex \
 # Build environment setup
 && apk add --no-cache --virtual .build-deps \
      autoconf \
      automake \
      build-base \
      c-ares-dev \
      cmake \
      git \
      libev-dev \
      libtool \
      libressl-dev \
      libsodium-dev \
      linux-headers \
      mbedtls-dev \
      mbedtls-static \
      pcre-dev \
      zlib-dev \
 # Build & install
 && cd /tmp/repo \
 && git clone --recursive https://github.com/shadowsocks/shadowsocks-libev.git \
 && cd shadowsocks-libev \
 && ./autogen.sh \
 && ./configure --prefix=/usr --disable-documentation \
 && make install \
 && apk del .build-deps \
 # Runtime dependencies setup
 && apk add --no-cache \
      rng-tools \
      $(scanelf --needed --nobanner /usr/bin/ss-* \
      | awk '{ gsub(/,/, "\nso:", $2); print "so:" $2 }' \
      | sort -u) \
 && rm -rf /tmp/repo

USER nobody

ENTRYPOINT [ "/usr/bin/ss-server" ]