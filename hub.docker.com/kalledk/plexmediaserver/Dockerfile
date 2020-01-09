FROM ubuntu:trusty

ENV LANG=C.UTF-8 \
    APT_GET_UPDATE=2016-04-04

RUN set -x \
    && PLEX_VERSION=0.9.16.3.1840-cece46d \
    && BUILD_DEPS=' \
        curl \
    ' \
    && RUN_DEPS=' \
        ca-certificates \
    ' \
    && DEBIAN_FRONTEND=noninteractive apt-get -q -y update \
    && DEBIAN_FRONTEND=noninteractive apt-get -q -y install ${BUILD_DEPS} ${RUN_DEPS} \
    && curl -SL -o plex.deb "https://downloads.plex.tv/plex-media-server/${PLEX_VERSION}/plexmediaserver_${PLEX_VERSION}_amd64.deb" \
    && dpkg -i plex.deb \
    && rm -f plex.deb \
    && apt-get purge -y --auto-remove ${BUILD_DEPS} \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/* 
