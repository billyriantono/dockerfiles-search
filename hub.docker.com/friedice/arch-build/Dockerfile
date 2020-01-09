FROM archlinux/base

RUN useradd -m -d /build -s /bin/bash build-user

RUN pacman -Sy --noconfirm base-devel cmake meson pacman-contrib
