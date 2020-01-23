FROM ubuntu:15.04

MAINTAINER Dreae <thedreae@gmail.com>

RUN apt-get install -y --no-install-recommends lib32gcc1 libstdc++ wget

RUN useradd -m steam

USER steam
WORKDIR /home/steam

RUN wget http://media.steampowered.com/installer/steamcmd_linux.tar.gz
RUN tar -xvzf steamcmd_linux.tar.gz
RUN /home/steam/steamcmd.sh +login anonymous +force_install_dir cstrike +app_update 232330 +exit

WORKDIR cstrike

EXPOSE 27015/udp

ENTRYPOINT ["./srcds_run", "-game cstrike", "-port 27015", "-console"]
