FROM bcit/centos:8-supervisord-latest

LABEL maintainer="jesse@weisner.ca"

ENV HOME /home/steam

RUN useradd steam \
 && yum -y --setopt tsflags=nodocs --setopt timeout=5 install \
        glibc.i686 \
        libstdc++.i686 \
        rsync \
        unzip \
        zip

COPY 20-install_steamcmd.sh /docker-entrypoint.d/
COPY 15-skel.sh /docker-entrypoint.d/
COPY ld-steamcmd.conf /etc/ld.so.conf.d/steamcmd.conf

RUN ldconfig

USER steam

VOLUME /home/steam

WORKDIR /home/steam
