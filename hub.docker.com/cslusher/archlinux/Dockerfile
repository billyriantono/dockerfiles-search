# Arch Linux
#
# VERSION 0.0.1

FROM base/archlinux
MAINTAINER Craig Slusher <cslush@gmail.com>

ADD mirrorlist /etc/pacman.d/mirrorlist

RUN pacman --noconfirm -Sy
RUN pacman --noconfirm -S pacman
RUN pacman-db-upgrade
