FROM oskarirauta/alpine:latest
MAINTAINER Oskari Rauta <oskari.rauta@gmail.com>

VOLUME /config
VOLUME /webroot

EXPOSE 80

ENV PUID=""
ENV PGID=""

RUN apk add --no-cache pcre bash shadow dcron tzdata ca-certificates libcap \
 && update-ca-certificates

RUN apk add --no-cache --repository "http://nl.alpinelinux.org/alpine/edge/main" \
      libressl2.5-libcrypto \
      libressl2.5-libssl \
      nginx

RUN mkdir /etc/nginx-default
RUN mkdir /etc/nginx-default/modules
RUN mkdir /etc/nginx-default/logs

COPY /config/ /etc/nginx-default/
COPY /init/nginx-serv /etc/init.d/nginx-serv
COPY /cron/root /etc/crontabs/root

RUN setcap CAP_NET_BIND_SERVICE=+eip /usr/sbin/nginx

RUN rm -rf /root/.cache

RUN rc-update add nginx-serv default
RUN rc-update add dcron default
