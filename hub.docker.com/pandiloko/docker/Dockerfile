
FROM base/archlinux:latest

RUN pacman  --needed  --noconfirm -Sy archlinux-keyring && \
    pacman-key --populate archlinux && \
    pacman -Syy  && pacman -S --needed --noconfirm --quiet  base-devel git wget yajl bind-tools git sudo xz gzip binutils unzip unrar grep fakeroot file cron wget vim iputils net-tools iproute awk bc pacman-contrib && \
    paccache -ruk0 && pacman -Scc --noconfirm && rm -rf /var/cache/pacman/pkg/*

RUN rmdir /opt && useradd jaime -Umd /opt -s /bin/bash && sudo sh -c "echo \"jaime ALL=(ALL) NOPASSWD:ALL\" >> /etc/sudoers" \
    && echo "en_US.UTF-8 UTF-8" >> /etc/locale.gen && echo LANG=en_US.UTF-8 >> /etc/locale.conf && locale-gen

USER jaime

RUN cd /tmp &&\
    git clone https://aur.archlinux.org/package-query.git && cd package-query && makepkg -si  --noconfirm  &&\
    git clone https://aur.archlinux.org/yaourt.git && cd yaourt && makepkg -si  --noconfirm

RUN wget static.pandiloko.com/bashrc -O ~/.bashrc && wget static.pandiloko.com/yaourtrc -O ~/.yaourtrc && source ~/.bashrc
