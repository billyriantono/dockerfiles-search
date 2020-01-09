FROM debian

MAINTAINER laninabox <info@utopit.be>

RUN dpkg --add-architecture i386 && \
     apt-get update && \
     apt-get upgrade -y && \
     apt-get install -y lib32gcc1 curl
RUN useradd -m steam -d /steam
 
RUN mkdir -p /steam/steamcmd_linux /steam/data && \
    curl -sqL 'https://steamcdn-a.akamaihd.net/client/installer/steamcmd_linux.tar.gz' | tar zxvf - -C /steam/steamcmd_linux 

RUN /steam/steamcmd_linux/steamcmd.sh +login anonymous +force_install_dir /steam/data +app_update 740 +quit

ADD files/start.sh /steam/data/.
ADD files/cfg/csgo-server.cfg /steam/data/csgo/cfg/
ADD files/cfg/esl/ /steam/data/csgo/cfg/
ADD files/motd.txt /steam/data/csgo/

RUN chown -R 1000:1000 /steam

WORKDIR /steam
USER steam

CMD ["./start.sh"]
