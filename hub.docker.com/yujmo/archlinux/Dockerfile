FROM base/archlinux:latest
ADD pacman.conf /etc/pacman.conf
RUN pacman -Sy && pacman -Syu --noconfirm && pacman -S man --noconfirm && pacman -S sed --noconfirm  && pacman -S yaourt --noconfirm \
    && echo "nameserver 114.114.114.114" > /etc/resolv.conf
ADD mirrorlist /etc/pacman.d/mirrorlist
RUN yaourt -Syy && yaourt -Syu --noconfirm 
