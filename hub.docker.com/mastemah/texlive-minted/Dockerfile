FROM archlinux/base

RUN    pacman-key --init \
    && pacman-key --populate archlinux \
    && pacman --noconfirm -Syu \
    && pacman --noconfirm -S base-devel \
    && pacman --noconfirm -S texlive-most biber minted \
    && rm -f \
       /var/cache/pacman/pkg/*

ENV PATH="/usr/bin/vendor_perl:${PATH}"
WORKDIR /data