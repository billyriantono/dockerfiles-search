FROM archlinux/base:latest

ARG VERSION="4.1.7-1"
LABEL build_version="qbittorrent-nox version:- ${VERSION}"
LABEL maintainer="tsubus"

# set environment variables
ENV HOME="/config/qbittorrent"

# volume
VOLUME /config /media

RUN \
    echo "**** install sonarr-ilwt ****" && \
    pacman -Syu --noconfirm && \
    pacman -S --noconfirm qbittorrent-nox

RUN \
    echo "**** Clean up ****" && \
    pacman -Scc --noconfirm && \
    rm -rf \
        /tmp/* \
        /var/tmp/*

CMD /usr/bin/qbittorrent-nox
