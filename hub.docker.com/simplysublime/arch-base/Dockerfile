FROM archlinux/base:latest
MAINTAINER simplysublime

ENV S6_OVERLAY_VERSION 1.22.1.0

COPY container-files /
COPY mirrorlist /etc/pacman.d/mirrorlist

RUN pacman --noconfirm -Syu && \
pacman --noconfirm -S wget tar && \
rm -rf /usr/share/man/* /var/cache/pacman/pkg/* /var/lib/pacman/sync/* /etc/pacman.d/mirrorlist.pacnew && \
cd /tmp && \
wget https://github.com/just-containers/s6-overlay/releases/download/v$S6_OVERLAY_VERSION/s6-overlay-amd64.tar.gz && \
tar xzf s6-overlay-amd64.tar.gz -C / && \
rm s6-overlay-amd64.tar.gz && \
sh /usr/local/sbin/fix-bins.sh

RUN pacman -Syy ranger htop neovim --noconfirm


ENTRYPOINT ["/init"]