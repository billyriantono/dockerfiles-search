FROM dock0/service
MAINTAINER Jon Chen <bsd@voltaire.sh>

EXPOSE 53/udp

RUN pacman -Syu --needed --noconfirm nsd
ADD run /service/nsd/run
