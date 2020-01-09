FROM debian:stretch-slim
MAINTAINER rbwsam 

RUN apt update && apt install -y lib32gcc1 curl lib32tinfo5
RUN useradd -m steam
USER steam
RUN mkdir /home/steam/steamcmd
WORKDIR /home/steam/steamcmd
RUN curl -sqL "https://steamcdn-a.akamaihd.net/client/installer/steamcmd_linux.tar.gz" | tar zxvf -
RUN ./steamcmd.sh +quit
