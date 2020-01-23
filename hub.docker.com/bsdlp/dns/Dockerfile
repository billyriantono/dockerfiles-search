FROM docku/nsd
MAINTAINER Jon Chen <bsd@voltaire.sh>

EXPOSE 53

RUN pacman -Syu --needed --noconfirm dnsutils

ADD nsd /srv/nsd
