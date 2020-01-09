FROM archlinux/base

copy ./config/mirrorlist /etc/pacman.d/mirrorlist

RUN pacman -Syy && pacman -S --noconfirm \
    neovim \
    git \
    python-neovim

RUN pacman -Scc --noconfirm
RUN rm -rf /tmp/*

ENTRYPOINT ["nvim"]
