FROM devkitpro/toolchain-base

RUN dkp-pacman -Syyu --noconfirm gamecube-dev wii-dev wiiu-dev devkitARM && \
    dkp-pacman -S --needed --noconfirm `dkp-pacman -Slq dkp-libs | grep '^ppc-'` && \
    dkp-pacman -Scc --noconfirm && \
    apt-get update && \
    apt-get install -y zip
ENV DEVKITPPC=${DEVKITPRO}/devkitPPC
ENV DEVKITARM=${DEVKITPRO}/devkitARM
