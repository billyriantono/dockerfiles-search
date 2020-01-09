FROM alpine

ARG VERSION="3.3.3"

WORKDIR /build

RUN apk add --no-cache build-base pcre-dev mbedtls-dev libsodium-dev c-ares-dev linux-headers libev-dev

RUN wget https://github.com/shadowsocks/shadowsocks-libev/releases/download/v${VERSION}/shadowsocks-libev-${VERSION}.tar.gz \
&& tar -zvxf shadowsocks-libev-${VERSION}.tar.gz \
&& cd /build/shadowsocks-libev-${VERSION} \
&& ./configure --prefix=/build --disable-documentation \
&& make install

FROM alpine
LABEL maintainer="Angdo"
EXPOSE 10800/tcp 10800/udp
WORKDIR /tunnel

COPY --from=0 /build/bin/ss-server /usr/bin

RUN apk add --no-cache libev c-ares pcre libsodium mbedtls \
&& wget https://bintray.dragon.ivenfe.cc/tunnel/default.json

ENTRYPOINT ["ss-server", "-s", "0.0.0.0", "-p", "10800","-u", "-c", "default.json"]
