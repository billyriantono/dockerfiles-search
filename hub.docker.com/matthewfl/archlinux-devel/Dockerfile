FROM      base/archlinux
MAINTAINER Matthew Francis-Landau <matthew@matthewfl.com>

RUN pacman -Syu --noconfirm --ignore filesystem

RUN pacman -S base-devel --noconfirm && rm -rf /var/cache/pacman/pkg

RUN cd /tmp && curl https://aur.archlinux.org/packages/pa/packer/packer.tar.gz | tar xz && cd /tmp/packer && makepkg -si --asroot --noconfirm && rm -rf /tmp/packer /var/cache/pacman/pkg