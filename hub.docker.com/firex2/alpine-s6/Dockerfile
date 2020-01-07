FROM alpine:3.6

MAINTAINER Fire

ENV S6_OVERLAY_VERSION=v1.19.1.1

RUN 	apk add --no-cache curl \
 	&& curl -L -s https://github.com/just-containers/s6-overlay/releases/download/${S6_OVERLAY_VERSION}/s6-overlay-amd64.tar.gz | tar xvzf - -C / \
 	&& apk del --no-cache curl

ADD rootfs /

ENTRYPOINT ["/init"]
