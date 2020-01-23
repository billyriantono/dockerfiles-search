FROM raz0red/devkit-toolchain-base

MAINTAINER Dave Murphy <davem@devkitpro.org>

VOLUME ["/source"]

RUN dkp-pacman -Syyu --noconfirm gamecube-dev wii-dev wiiu-dev && \
    dkp-pacman -S --needed --noconfirm `dkp-pacman -Slq dkp-libs | grep '^ppc-'` && \
    dkp-pacman -Scc --noconfirm
ENV DEVKITPPC=${DEVKITPRO}/devkitPPC
