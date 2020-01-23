FROM base/archlinux

ADD https://www.archlinux.org/mirrorlist/all/http /tmp/mirrorlist
RUN cat /tmp/mirrorlist | cut -c2- > /etc/pacman.d/mirrorlist && \
    pacman -Sy archlinux-keyring --noconfirm && \
    pacman -S pacman --noconfirm && pacman-db-upgrade && \
    pacman -Syu --noconfirm && \
    pacman -S base-devel git --noconfirm && \
    chmod +r /etc/pacman.d/mirrorlist

ENTRYPOINT /usr/bin/bash
