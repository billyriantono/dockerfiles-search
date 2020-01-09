FROM archlinux/base:latest

LABEL maintainer="Gabriel Tiossi"
LABEL ansible_os_family="Archlinux"

ENV GOSS_VER=v0.3.7
ENV GOSS_DST=/usr/bin

RUN pacman -Sy \
 && pacman -S --noconfirm python openssh curl \
 && curl -fsSL https://goss.rocks/install | sh \
 && pacman -Scc --noconfirm
