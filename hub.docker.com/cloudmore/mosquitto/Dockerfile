FROM alpine

EXPOSE 1883 8883

ARG APK_CACHE_IP=172.17.0.1
ARG APK_CACHE_DOMAIN='dl-cdn.alpinelinux.org www.lua.org'

ARG RUN_DEPS='mosquitto mosquitto-libs lua5.2 openssl-dev'
ARG BUILD_DEPS='coreutils tar git libc-dev gcc make lua5.2-dev mosquitto-dev c-ares-dev'

#ARG LUA_VERSION=5.3.4
ARG LUA_URL='http://www.lua.org/ftp'
ARG LUA_TMP=/tmp/lua

#ARG MOSQUITTO_VERSION=1.4.11
ARG MOSQUITTO_URL='http://mosquitto.org/files/source'
ARG MOSQUITTO_TMP=/tmp/mosquitto
ENV MOSQUITTO_HOME=/opt/mosquitto

RUN nc -z $APK_CACHE_IP 80 && echo $APK_CACHE_IP $APK_CACHE_DOMAIN >>/etc/hosts \
 ; apk --update add --no-cache $RUN_DEPS $BUILD_DEPS \
  && git clone https://github.com/DenkiYagi/lua_auth_plugin.git \
  && cd lua_auth_plugin \
  && make \
     CFLAGS='-std=gnu99 -fPIC -I../include/ -L../lib/x86_64-linux-gnu/ -Wall -Wextra -O2 -I/usr/include/lua5.2' \
     LIBS='-L/usr/lib/lua5.2 -llua -ldl -lmosquitto -lssl -lcares' \
  && make install \
 && apk del $BUILD_DEPS && rm -rf /var/cache/apk/*

WORKDIR /etc/mosquitto

ADD . .

CMD ["mosquitto","-c","/etc/mosquitto/mosquitto.conf"]
