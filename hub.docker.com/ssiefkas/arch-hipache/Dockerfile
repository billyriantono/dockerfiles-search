FROM ssiefkas/arch-base:latest
MAINTAINER Shawn Siefkas <shawn@siefk.as>

RUN pacman --noconfirm -Sy nodejs git
RUN npm install hipache -g
ADD hipache.cfg /srv/hipache/
ADD start.sh /srv/hipache/

WORKDIR /srv/hipache
CMD ./start.sh
