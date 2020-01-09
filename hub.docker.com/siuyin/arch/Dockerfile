FROM archlinux/base
RUN pacman -Sy --noconfirm git vim sudo tmux go file
RUN useradd -u 1000 -m siuyin && echo "siuyin ALL=(ALL) NOPASSWD:ALL" > /etc/sudoers.d/siuyin
