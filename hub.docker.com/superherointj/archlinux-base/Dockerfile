FROM archlinux
RUN echo 'Server = https://mirror.osbeck.com/archlinux/$repo/os/$arch' > /etc/pacman.d/mirrorlist
# Upgrade system
RUN pacman -Syu --noconfirm