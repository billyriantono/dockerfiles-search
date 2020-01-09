FROM archlinux/base

RUN pacman -Sy \
 && pacman -S --noconfirm binutils grep mlocate awk git vim pacman-contrib \
 && pacman -Scc --noconfirm

RUN useradd -m -U -s /bin/bash archlinux
RUN mkdir /aur \
 && chown -R archlinux:archlinux /aur

USER archlinux
WORKDIR /aur
