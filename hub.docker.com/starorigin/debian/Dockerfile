FROM debian:stable

ENV DATA_PATH /data

COPY sources.list /etc/apt/

RUN mkdir $DATA_PATH \
 && DEBIAN_FRONTEND=noninteractive \
 apt-get update \
 && DEBIAN_FRONTEND=noninteractive \
 apt-get -y install apt-utils \
 && DEBIAN_FRONTEND=noninteractive \
 apt-get -y upgrade \
 && dpkg -l | grep '^ii' | awk '{print $2}' > /data/pkg.txt
