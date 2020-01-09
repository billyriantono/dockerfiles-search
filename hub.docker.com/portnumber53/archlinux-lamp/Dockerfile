FROM base/archlinux

# Updating keys and system
RUN pacman -Sy --noconfirm archlinux-keyring
RUN pacman-key --init && pacman-key --populate archlinux && pacman-key --refresh-keys
RUN pacman -Syu --noconfirm
