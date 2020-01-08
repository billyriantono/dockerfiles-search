# mcserver
# Minecraft Server based on itzg's work 
# Version 0.0.3

FROM java:8

ENTRYPOINT ["supervisord"]

ADD supervisord.ini /etc/supervisor/conf.d/supervisord.conf

VOLUME ["/mcserver"]

EXPOSE 25565

ENV APT_GET_UPDATE 2015-10-03
RUN apt-get update

RUN DEBIAN_FRONTEND=noninteractive apt-get install -y \
  libmozjs-24-bin \
  imagemagick \
  lsof \
  supervisor \
  && apt-get clean
RUN update-alternatives --install /usr/bin/js js /usr/bin/js24 100

RUN wget -O /usr/bin/jsawk https://github.com/micha/jsawk/raw/master/jsawk
RUN chmod +x /usr/bin/jsawk

# Special marker ENV used by MCCY management tool
ENV MC_IMAGE=YES

ENV UID=1000 GID=1000
ENV MOTD David's Minecraft Server Powered by Docker
ENV JVM_OPTS -Xmx1024M -Xms1024M
ENV TYPE=VANILLA VERSION=LATEST FORGEVERSION=RECOMMENDED LEVEL=world PVP=true DIFFICULTY=easy \
  LEVEL_TYPE=DEFAULT GENERATOR_SETTINGS= WORLD= MODPACK=
