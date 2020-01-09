FROM golang:alpine AS builder
ARG GCSFUSE_VERSION=0.27.0
RUN apk --update --no-cache add git fuse fuse-dev
RUN go get -d github.com/googlecloudplatform/gcsfuse
RUN go install github.com/googlecloudplatform/gcsfuse/tools/build_gcsfuse
RUN build_gcsfuse ${GOPATH}/src/github.com/googlecloudplatform/gcsfuse /tmp ${GCSFUSE_VERSION}

FROM lsiobase/alpine:3.10

# set version label
ARG BUILD_DATE
ARG VERSION
ARG QBITTORRENT_VERSION
LABEL build_version="Linuxserver.io version:- ${VERSION} Build-date:- ${BUILD_DATE}"
LABEL maintainer="sparklyballs, thelamer"

# environment settings
ENV HOME="/config" \
XDG_CONFIG_HOME="/config" \
XDG_DATA_HOME="/config"

# add repo and install qbitorrent
RUN echo "http://dl-cdn.alpinelinux.org/alpine/edge/main/" >> /etc/apk/repositories && \
    echo "http://dl-cdn.alpinelinux.org/alpine/edge/testing/" >> /etc/apk/repositories && \
    apk update && \
    apk add --no-cache \
      geoip \
      qbittorrent-nox \
      fuse && \
    rm -rf /tmp/*

# add local files
COPY root/ /
COPY --from=builder /tmp/bin/gcsfuse /bin
COPY --from=builder /tmp/sbin/mount.gcsfuse /sbin
RUN ln -s mount.gcsfuse /sbin/mount.fuse.gcsfuse

# ports and volumes
EXPOSE 6881 6881/udp 8080
VOLUME /config /downloads/incomplete
