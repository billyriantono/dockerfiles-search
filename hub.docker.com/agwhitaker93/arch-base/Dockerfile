FROM archlinux

RUN pacman -Sy --noconfirm
RUN pacman -Syu base-devel --noconfirm
RUN pacman -Syu git --noconfirm

RUN useradd -m arch && \
    echo "arch:arch" | chpasswd \
    && echo "arch ALL=(ALL) NOPASSWD :ALL" >> /etc/sudoers
USER arch

RUN git clone https://aur.archlinux.org/yay.git /home/arch/aur/yay && \
    cd /home/arch/aur/yay && \
    makepkg -si --noconfirm && \
    rm -rf /home/arch/aur/yay

RUN mkdir /home/arch/app
WORKDIR /home/arch/app
