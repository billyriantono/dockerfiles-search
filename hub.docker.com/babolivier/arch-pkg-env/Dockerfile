FROM base/archlinux

RUN sed -i 's/^SigLevel    = Required DatabaseOptional/SigLevel = Never/' /etc/pacman.conf
RUN pacman -Syu --noconfirm
RUN pacman-db-upgrade
RUN pacman -S base-devel --noconfirm
RUN useradd pkg -m -d /pkg
RUN echo "pkg ALL=NOPASSWD: ALL" >> /etc/sudoers

USER pkg
WORKDIR /pkg

ENTRYPOINT makepkg -si --noconfirm && /pkg/tests
