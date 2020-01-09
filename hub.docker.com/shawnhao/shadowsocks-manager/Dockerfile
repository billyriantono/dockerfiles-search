#
# Dockerfile for shadowsocks-libev
#

FROM alpine
LABEL maiter="Shawn Hao"

ENV BUILD_DEPS git asciidoc xmlto
ENV RUNTIME_DEPS    autoconf automake build-base c-ares-dev libev-dev libtool libsodium-dev linux-headers mbedtls-dev pcre-dev
ENV SSSDIR     /tmp/shadowsocks-libev
ENV PORT  8399
ENV TIMEOUT    300
ENV DNS_ADDRS  1.1.1.1,8.8.8.8,8.8.4.4

# Set up building environment
RUN set -x \
 && apk add --no-cache --virtual .build-deps ${BUILD_DEPS} ${RUNTIME_DEPS} \
# Get the latest shadowsocks-libev code, build and install
 && git clone https://github.com/shadowsocks/shadowsocks-libev.git ${SSSDIR} \
 && cd ${SSSDIR} && git submodule update --init --recursive \
 &&./autogen.sh \
 && ./configure --prefix=/usr --disable-documentation \
 && make \
 && make install \
 && apk del .build-deps \
# Runtime dependencies setup
 && apk add --no-cache \
      rng-tools \
      $(scanelf --needed --nobanner /usr/bin/ss-* \
      | awk '{ gsub(/,/, "\nso:", $2); print "so:" $2 }' \
      | sort -u) \
 && rm -rf ${SSSDIR}

EXPOSE ${PORT}
WORKDIR /etc/shadowsocks-libev
COPY config.json ./config.json

CMD exec ss-manager \
      --manager-address 0.0.0.0:${PORT} \
      -uv -m aes-256-cfb \
      --fast-open \
      -d ${DNS_ADDRS} \
      -t ${TIMEOUT} \
      -c ./config.json