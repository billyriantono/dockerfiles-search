FROM archlinux/base:latest

RUN pacman -Syu --needed --noconfirm base-devel git go vim wget

COPY makepkg.conf /etc/makepkg.conf

RUN groupadd --gid 1000 developer \
    && useradd -rm --uid 1000 --gid 1000 developer \
    && echo 'developer ALL=(ALL) NOPASSWD:ALL' >> /etc/sudoers

ENV AURGIT https://aur.archlinux.org

USER developer
WORKDIR /home/developer
CMD ["/usr/bin/bash"]

