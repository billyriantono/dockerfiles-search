FROM tsubus/archlinux

ARG VERSION="5.4"
LABEL build_version="fitbit-steps version:- ${VERSION}"
LABEL maintainer="tsubus"

# set environment variables
ENV HOME="/config"

# volume
VOLUME /config

RUN \
    echo "**** install dependencies ****" && \
    pacman -Syu --noconfirm && \
    pacman -S --noconfirm \
    screen \
    tsubus-tools

RUN \
    echo "**** Clean up ****" && \
    pacman -Scc --noconfirm && \
    rm -rf \
    /tmp/* \
    /var/tmp/*

# add local files
COPY root/ /
