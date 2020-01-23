FROM alpine:latest
MAINTAINER MiX <mixchatmix3@gmail.com>

RUN set -xe \
    && apk add --no-cache --update bash \
    && apk add --no-cache --update aria2 && adduser -D -g '' pi

EXPOSE 6800
USER pi
VOLUME ["/home/aria2"]
VOLUME ["/home/aria2/downloads"]

CMD ["/usr/bin/aria2c","--enable-rpc", "--rpc-listen-all", "--conf-path=/home/aria2/aria2.conf"]
