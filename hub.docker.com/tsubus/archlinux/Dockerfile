FROM archlinux/base:latest
LABEL maintainer=tsubus
ARG BUILD_DATE="20191108"
LABEL build_version="Archlinux base + s6 overlay, build date: ${BUILD_DATE}"

# add local files
COPY root/ /

# environment variables
ENV PS1="$(whoami):$(pwd)\\$ " \
HOME="/root" \
TERM="xterm"

# install necessary packages
RUN \
    echo "**** update all packages ****" && \
    pacman -Syu --noconfirm && \
    pacman -S --noconfirm tar

# install s6-overlay
ARG OVERLAY_VERSION="v1.22.1.0"
ADD https://github.com/just-containers/s6-overlay/releases/download/${OVERLAY_VERSION}/s6-overlay-amd64.tar.gz /tmp/
RUN \
    echo "**** install s6-overlay ****" && \
    tar xzf /tmp/s6-overlay-amd64.tar.gz -C / && \
    echo "**** create abc user and make our folders ****" && \
    groupmod -g 1000 users && \
    useradd -u 911 -U -d /config -s /bin/false abc && \
    usermod -G users abc && \
    mkdir -p \
        /app \
        /config \
        /defaults && \
    echo "**** make /bin/sh symlink ****" && \
    ln -s /usr/sbin/sh /bin/sh && \
    echo "**** clean up ****" && \
    pacman -R --noconfirm tar && \
    pacman -Scc --noconfirm && \
    rm -rf \
        /tmp/* \
        /var/tmp/*

ENTRYPOINT ["/init"]
