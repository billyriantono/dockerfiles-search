FROM debian:wheezy

MAINTAINER Chris Daish <chrisdaish@gmail.com>

ENV DEBIAN_FRONTEND noninteractive

RUN useradd -m steam; \
    apt-get update; \
    apt-get install -y wget lib32gcc1; \
    rm -rf /var/lib/apt/lists/*

USER steam

WORKDIR /home/steam

RUN wget -q http://media.steampowered.com/installer/steamcmd_linux.tar.gz; \
    tar -xzf steamcmd_linux.tar.gz; \
    rm -f steamcmd_linux.tar.gz

CMD ["/home/steam/steamcmd.sh", "+login", "anonymous", "+quit"]
