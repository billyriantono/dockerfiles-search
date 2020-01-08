FROM archlinux/base:latest

ARG VERSION="20191229.18.31"
LABEL build_version="radarr-ilwt version:- ${VERSION}"
LABEL maintainer="tsubus"

# set environment variables
ENV HOME="/config/radarr"

# volume
VOLUME /config /media

# add local files
COPY root/ /

RUN \
    echo "**** install radarr-ilwt ****" && \
    pacman -Syu --noconfirm && \
    pacman -S --noconfirm radarr-ilwt && \
    echo "**** Clean up ****" && \
    pacman -Scc --noconfirm && \
    rm -rf \
        /tmp/* \
        /var/tmp/*

CMD /usr/bin/radarr -nobrowser -data=/config/radarr/data
