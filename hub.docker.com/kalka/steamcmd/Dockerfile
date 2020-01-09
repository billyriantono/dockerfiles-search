FROM ubuntu:16.04

LABEL maintainer="Kalka <k@kalka.io>"

RUN mkdir -p /opt/steamcmd

ENV DEBIAN_FRONTEND=noninteractive

RUN dpkg --add-architecture i386 && \
    apt-get update && \
    apt-get install -y \
    ca-certificates \
    lib32tinfo5 && \
    echo debconf steam/question select I AGREE | debconf-set-selections && \
    apt-get install -y steamcmd && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*


RUN useradd -m steam

USER steam

RUN /usr/games/steamcmd +login anonymous +quit

ENTRYPOINT ["/usr/games/steamcmd"]
