FROM ubuntu:16.04
MAINTAINER Romain Deville <romaindeville1@gmail.com>

ARG OVERLAY_VERSION="v1.18.1.5"
ARG OVERLAY_ARCH="amd64"

ENV \
# set evironment variable
  DEBIAN_FRONTEND="noninteractive" \
  HOME="/root" \
  TERM="xterm"

# add some files
COPY sources.list /etc/apt/sources.list
ADD https://github.com/just-containers/s6-overlay/releases/download/${OVERLAY_VERSION}/s6-overlay-${OVERLAY_ARCH}.tar.gz /tmp/

RUN \
# install main package
  apt-get update && \
  apt-get install -y \
    apt-utils && \
  apt-get upgrade -y && \

# add s6 overlay
  tar xfz /tmp/s6-overlay-${OVERLAY_ARCH}.tar.gz -C / && \

# crete user
  useradd -u 911 -U -d /config -s /bin/false imgusr && \
  usermod -G users imgusr && \

# create folder
  mkdir -p \
    /app \
    /config \
    /defaults

COPY root/ /tmp/root/

RUN \
# avoid docker hub error because of copying to /
  cp -r /tmp/root/* / && \
# cleanup
  apt-get clean && \
  rm -rf \
    /var/lib/apt/lists/* \
    /tmp/* \
    /var/tmp/*

CMD ["/init"]
