# base image
FROM kmallea/csgo:latest

MAINTAINER Alexandre Croteau-Pothier <alex@alexcp.com>

USER root
RUN apt-get update && apt-get install wget

RUN cd /home/steam/csgo/csgo
RUN wget http://www.gsptalk.com/mirror/sourcemod/mmsource-1.10.6-linux.tar.gz
RUN tar xzf mmsource-1.10.6-linux.tar.gz
RUN wget http://www.sourcemod.net/smdrop/1.7/sourcemod-1.7.3-git5301-linux.tar.gz
RUN tar xzf sourcemod-1.7.3-git5301-linux.tar.gz

RUN cd /home/steam/steamcmd &&\
    ./steamcmd.sh \
    +login anonymous \
    +force_install_dir ../csgo \
    +app_update 740 validate \
    +quit

USER steam
WORKDIR /home/steam/csgo

CMD ["-game csgo -console -nohltv -tickrate 128 -usercon +game_type 0 +game_mode 0 +mapgroup mg_bomb +map de_dust2"]