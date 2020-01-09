FROM alpine:3.10
MAINTAINER Mikkel Oscar Lyderik Larsen <m@moscar.net>

# install runtime packages
RUN \
 apk add --no-cache \
    ca-certificates \
    p7zip \
    unrar \
    unzip && \
 apk add --no-cache \
    --repository=http://dl-cdn.alpinelinux.org/alpine/edge/main \
    --repository=http://dl-cdn.alpinelinux.org/alpine/edge/community \
    --repository=http://dl-cdn.alpinelinux.org/alpine/edge/testing \
    deluge && \

# cleanup
 rm -rf \
    /root/.cache
