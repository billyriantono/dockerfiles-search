
FROM alpine:latest
LABEL maintainer="docker@mcxiaoke.com"

ENV LIBEV_VERSION 3.3.1

ENV SERVER_ADDR 0.0.0.0
ENV SERVER_PORT 9001
ENV PASSWORD=
ENV METHOD      aes-256-cfb
ENV TIMEOUT     300
ENV DNS_ADDRS    8.8.8.8,8.8.4.4
ENV ARGS=

#ENV FILE_URL https://github.com/shadowsocks/shadowsocks-libev/releases/download/v${LIBEV_VERSION}/\
#shadowsocks-libev-${LIBEV_VERSION}.tar.gz
#ENV FILE_URL https://github.com/shadowsocks/shadowsocks-libev/archive/v${LIBEV_VERSION}.zip
#COPY . /tmp/repo

RUN set -ex \
 # Change alpinelinux source
 #&& sed -i 's/dl-cdn.alpinelinux.org/mirrors.ustc.edu.cn/g' /etc/apk/repositories \
 #&& echo http://mirrors.ustc.edu.cn/alpine/v3.10/main > /etc/apk/repositories \
 #&& echo http://mirrors.ustc.edu.cn/alpine/v3.10/community >> /etc/apk/repositories \
 # Build environment setup
 && apk add --no-cache --virtual .build-deps \
      git \
      autoconf \
      automake \
      build-base \
      c-ares-dev \
      libev-dev \
      libtool \
      libsodium-dev \
      linux-headers \
      mbedtls-dev \
      pcre-dev \
# Prepare source files
 && mkdir -p /tmp/xxx \
 && cd /tmp/xxx \
# &&  curl -SL# ${FILE_URL} | tar zxf - -C /tmp/xxx \
# && wget ${FILE_URL} -O f.zip \
# && unzip f.zip \
# && cd shadowsocks-libev-${LIBEV_VERSION} \
&& git clone --recursive https://github.com/shadowsocks/shadowsocks-libev.git \
&& cd shadowsocks-libev \
&& git checkout v${LIBEV_VERSION} \
 # Build & install
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
 && rm -rf /tmp/xxx

USER nobody

CMD exec ss-server \
      -s $SERVER_ADDR \
      -p $SERVER_PORT \
      -k ${PASSWORD:-$(hostname)} \
      -m $METHOD \
      -t $TIMEOUT \
      -d $DNS_ADDRS \
      -u \
      $ARGS
