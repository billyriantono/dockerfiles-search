FROM archlinux/base:latest

ARG VERSION="20200105.17.50"
LABEL build_version="sonarr-ilwt version:- ${VERSION}"
LABEL maintainer="tsubus"

# set environment variables
ENV HOME="/config/sonarr"

# volume
VOLUME /config /media

# add local files
COPY root/ /

RUN \
    echo "**** install sonarr-ilwt ****" && \
    pacman -Syu --noconfirm && \
    pacman -S --noconfirm sonarr-ilwt && \
    echo "UpdateMethod=docker" > /usr/lib/sonarr/package_info && \
    echo "Branch=phantom-develop" >> /usr/lib/sonarr/package_info && \
    echo "PackageVersion=${VERSION}" >> /usr/lib/sonarr/package_info && \
    echo "PackageAuthor=tsubus" >> /usr/lib/sonarr/package_info && \
    echo "**** Clean up ****" && \
    pacman -Scc --noconfirm && \
    rm -rf \
        /tmp/* \
        /var/tmp/*

CMD /usr/bin/sonarr -nobrowser -data=/config/sonarr/data
