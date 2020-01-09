FROM base/archlinux
RUN pacman -Sy
# Updates the keyring so we can install packages.
RUN pacman -S --noconfirm --needed archlinux-keyring
# Installs dev tools and fixes an OpenSSL-related missing symbol bug.
RUN pacman -S --noconfirm --needed base-devel openssl
# Updates pacman db format
RUN pacman-db-upgrade