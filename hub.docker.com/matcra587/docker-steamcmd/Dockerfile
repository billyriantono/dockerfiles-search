FROM ubuntu:18.04 AS build

RUN sed -i "/^# deb.*multiverse/ s/^# //" /etc/apt/sources.list \
    && dpkg --add-architecture i386 \
    && apt-get update -qq \
    && echo steam steam/question select "I AGREE" | debconf-set-selections \
    && echo steam steam/license note '' | debconf-set-selections \
    && apt-get install -qq ca-certificates steamcmd > /dev/null \
    && rm -rf /var/lib/apt/lists/*

FROM scratch

LABEL version="1.0.0"
LABEL vendor="Sistemics Esports"
LABEL maintainer="mcraven@sistemics.uk"
LABEL release-date="15.07.2018"
LABEL version.is-production="yes"
LABEL description="Ubuntu Image with steamcmd installed by \
    the package manager"

ENV PATH="/usr/games/:${PATH}"

WORKDIR /

COPY --from=0 / .
