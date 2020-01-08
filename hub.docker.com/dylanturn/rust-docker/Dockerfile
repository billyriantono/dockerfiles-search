FROM centos:7.3.1611
MAINTAINER Dylan Turnbull <dylanturn@gmail.com>

ENV SERVER_IP 0.0.0.0
ENV SERVER_PORT 28015
ENV RCON_PORT 28016
ENV RCON_PASSWORD rconPass01
ENV PLAYER_LIMIT 75
ENV SERVER_NAME "Rusty Whale"
ENV SERVER_ID change_me
ENV LEVEL_TYPE "Procedural Map" 
ENV LEVEL_SEED 80808
ENV WORLD_SIZE 3000
ENV SAVE_INTERVAL 300
ENV GLOBAL_CHAT_ENABLED true
ENV SERVER_DESCRIPTION "This server is a WHALE of a time! Try to CONTAIN yourself!"
ENV HEADER_IMAGE_LINK https://raw.githubusercontent.com/docker-library/docs/c350af05d3fac7b5c3f6327ac82fe4d990d8729c/docker/logo.png
ENV WEBSITE_LINK http://www.google.com
ENV RUST_PATH /opt/rust

RUN yum -y install glibc.i686 libstdc++.i686 wget nano tar screen

RUN mkdir $RUST_PATH
ADD startrust.sh $RUST_PATH
RUN chmod -v +x $RUST_PATH/startrust.sh

RUN mkdir /opt/steam
ADD runscript /opt/steam/runscript

VOLUME $RUST_PATH

RUN cd /opt/steam && \
    wget https://steamcdn-a.akamaihd.net/client/installer/steamcmd_linux.tar.gz && \
    tar xf steamcmd_linux.tar.gz && \
    ./steamcmd.sh +runscript runscript

WORKDIR $RUST_PATH
CMD ["startrust.sh"]