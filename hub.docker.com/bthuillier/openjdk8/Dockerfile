FROM base/archlinux:latest
MAINTAINER Benjamin Thuillier <benjaminthuillier@gmail.com>

RUN mkdir /project

WORKDIR /project

RUN pacman --noconfirm -Sy jdk8-openjdk ca-certificates openssl wget; yes | pacman -Scc
