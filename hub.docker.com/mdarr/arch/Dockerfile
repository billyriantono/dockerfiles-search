from archlinux/base

RUN pacman --noconfirm -Syuq \
        base-devel \
        git \
        go \
        sudo \
    && groupadd -g 666 archie \
    && useradd -m -r -G adm,sys,users,wheel -u 666 -g archie archie \
    && mkdir -p /packages \
    && chown -R archie /packages \
    && echo -e "BUILDDIR=/packages\nPKGDEST=/packages\nSRCDEST=/packages\nSRCPKGDEST=/packages\nLOGDEST=/packages" >> /etc/makepkg.conf \
    && echo -e "archie   ALL=(ALL) ALL\nDefaults:archie      !authenticate" >> /etc/sudoers.d/archie \
    && chmod 440 /etc/sudoers.d/archie \
    && pacman -Scc \
    && rm -rf /packages/*

USER archie
WORKDIR /home/archie
RUN git clone https://aur.archlinux.org/yay-git.git yay-git \
    && cd yay-git \
    && makepkg -sic --noconfirm \
    && rm -rf yay-git