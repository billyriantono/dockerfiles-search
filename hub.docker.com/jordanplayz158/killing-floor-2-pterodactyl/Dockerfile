# ----------------------------------
# Pterodactyl Core Dockerfile
# Environment: SteamCMD
# Minimum Panel Version: 0.6.0
# Original Dockerfile: https://github.com/dwurf/docker-kf2/blob/master/Dockerfile
# ----------------------------------
FROM ubuntu:xenial

MAINTAINER JordanPlayz158, <JordanPlayz158again@gmail.com>

RUN \
	apt-get -y update && \
	apt-get -y install curl ca-certificates openssl git tar bash sqlite fontconfig wget lib32gcc1 && \
	apt-get clean && \
	find /var/lib/apt/lists -type f | xargs rm -vf

RUN useradd -m -r -g root container
RUN chown -R container:root /home/container

USER container
ENV  USER=container HOME=/home/container

WORKDIR /home/container

ADD kf2_functions.sh /home/container/kf2_functions.sh
ADD main /home/container/main
ADD main.firststart /home/container/main.firststart

# Steam port
EXPOSE 20560/udp

# Query port - used to communicate with the master server
EXPOSE 27015/udp

# Game port - primary comms with players
EXPOSE 7777/udp

# Web Admin port
EXPOSE 8080/tcp

ENTRYPOINT ["/bin/bash", "main"]
