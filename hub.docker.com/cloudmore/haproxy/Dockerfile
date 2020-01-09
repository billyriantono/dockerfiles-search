FROM alpine:3.5

EXPOSE 80 443

ARG APK_CACHE_IP=172.17.0.1
ARG APK_CACHE_DOMAIN='dl-cdn.alpinelinux.org www.lua.org www.haproxy.org'

ARG RUN_DEPS='pcre openssl'
ARG BUILD_DEPS='pcre-dev openssl-dev zlib-dev readline-dev libc-dev gcc make linux-headers coreutils tar'

#ARG LUA_VERSION=5.3.3
ARG LUA_URL='http://www.lua.org/ftp'
ARG LUA_TMP=/tmp/lua
ENV LUA_HOME=/opt/lua

#ARG HAPROXY_VERSION=1.7.0
ARG HAPROXY_URL='http://www.haproxy.org'
ARG HAPROXY_TMP=/tmp/haproxy
ENV HAPROXY_CONF=/etc/haproxy

RUN nc -z $APK_CACHE_IP 80 && echo $APK_CACHE_IP $APK_CACHE_DOMAIN >>/etc/hosts \
  ; apk --update add --no-cache $RUN_DEPS $BUILD_DEPS \
    && LUA_LATEST=$(wget -qO- $LUA_URL | egrep -o "[0-9]+\.[0-9]+\.[0-9]+" | sort -Vr | head -1) \
    && mkdir -p $LUA_TMP && cd $LUA_TMP \
    && wget -qO- $LUA_URL/lua-${LUA_VERSION:=$LUA_LATEST}.tar.gz | tar xz --strip-components=1 \
    && make -j$(nproc) linux \
    && make install INSTALL_TOP=$LUA_HOME && cd / \
    && HAPROXY_LATEST=$(wget -qO- $HAPROXY_URL | egrep -o "[0-9]+\.[0-9]+\.[0-9]+" | sort -Vr | head -1) \
    && mkdir -p $HAPROXY_TMP && cd $HAPROXY_TMP \
    && : ${HAPROXY_VERSION:=$HAPROXY_LATEST} \
    && wget -qO- $HAPROXY_URL/download/${HAPROXY_VERSION%.*}/src/haproxy-$HAPROXY_VERSION.tar.gz | tar xz --strip-components=1 \
    && make -j$(nproc)  \
       TARGET=linux2628 USE_PCRE=1 USE_PCRE_JIT=1 PCREDIR= USE_OPENSSL=1 USE_ZLIB=1 USE_TFO=1 \
       USE_LUA=yes LUA_LIB=$LUA_HOME/lib/ LUA_INC=$LUA_HOME/include/ \
       all \
    && make install-bin \
    && mkdir -p $HAPROXY_CONF && cp -R examples/errorfiles $HAPROXY_CONF/errors \
  && cd / && rm -rf $LUA_TMP $HAPROXY_TMP && apk del $BUILD_DEPS && rm -rf /var/cache/apk/*

WORKDIR $HAPROXY_CONF

ADD . .

CMD ["haproxy","-f","/etc/haproxy/haproxy.cfg"]
