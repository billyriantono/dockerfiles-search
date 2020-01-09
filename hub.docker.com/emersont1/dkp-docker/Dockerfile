FROM archlinux/base

ENV DEVKITPRO=/opt/devkitpro
ENV DEVKITARM=/opt/devkitpro/devkitARM
ENV DEVKITPPC=/opt/devkitpro/devkitPPC

RUN pacman -Syu --noconfirm git cmake base-devel; \
pacman-key --init; \
pacman-key --recv F7FD5492264BB9D0; \
pacman-key --lsign F7FD5492264BB9D0; \
pacman -U --noconfirm https://downloads.devkitpro.org/devkitpro-keyring-r1.787e015-2-any.pkg.tar.xz; \
printf "[dkp-libs]\nServer = https://downloads.devkitpro.org/packages\n[dkp-linux]\nServer = https://downloads.devkitpro.org/packages/linux\n" >> /etc/pacman.conf; \
sudo pacman -Sy --noconfirm gba-dev cmake; 
