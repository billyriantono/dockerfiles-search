FROM ubuntu

WORKDIR /root

RUN apt-get update && apt-get install -y aria2 bzip2 curl wget && rm -rf /var/cache/apt
RUN aria2c --seed-time=0 --seed-ratio=0 http://redeclipse.net/files/releases/redeclipse_1.5.3_nix.tar.bz2.torrent && tar xjf redeclipse_1.5.3_nix.tar.bz2 \
    && mv redeclipse-1.5.3 redeclipse \
    && rm redeclipse_1.5.3_nix.tar.bz2* && rm -Rf /tmp/*

WORKDIR /root/redeclipse

RUN cp doc/examples/servinit.cfg .

RUN ./bin/update.sh

EXPOSE 28801/udp
EXPOSE 28802/udp

CMD ["/bin/bash", "./redeclipse_server.sh"]
