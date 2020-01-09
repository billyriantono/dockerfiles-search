FROM archlinux/base

WORKDIR /
LABEL maintainer=codehz
ADD . /

RUN pacman -Syu --needed --noconfirm python pyalpm rsync base-devel git util-linux systemd-libs
