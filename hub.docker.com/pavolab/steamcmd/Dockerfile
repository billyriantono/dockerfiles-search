FROM ubuntu:18.04

MAINTAINER Pavolab <https://github.com/Pavolab>

ARG STEAMCMD_URL=https://steamcdn-a.akamaihd.net/client/installer/steamcmd_linux.tar.gz
ARG STEAMCMD_HASH=cfc463be19d2a305412b897b050a3a94c81ddbf6

RUN apt-get update && apt-get install -y \
        lib32stdc++6 \
        lib32gcc1 \
        curl \
        ca-certificates \
        && apt-get -y upgrade \
        && apt-get clean autoclean \
        && apt-get autoremove -y \
        && mkdir -p /opt/steamcmd \
        && useradd -m steam \
        && chown -R steam /opt \
        && chmod -R 744 /opt

USER steam

RUN cd /opt/steamcmd/ \
    && curl -sqL "${STEAMCMD_URL}" | tar zxvf - \
    && rm -rf /var/lib/{apt,dpkg,cache,log} /tmp/* steamcmd_linux.tar.gz 

VOLUME [ "/opt/steamcmd" ]

ENTRYPOINT ["/opt/steamcmd/steamcmd.sh"]