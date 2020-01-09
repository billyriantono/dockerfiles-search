FROM archlinux/base:latest
# run xhost +si:localuser:$USER before running the image
MAINTAINER Abraham Finch <abraham@odinfinch.xyz>
ENV DISPLAY :0
ENV NO_AT_BRIDGE=1

RUN pacman -Sy --noconfirm awk sed pacman-contrib && \
cp /etc/pacman.d/mirrorlist /etc/pacman.d/mirrorlist.bak  && \
sed -i 's/^#Server/Server/' /etc/pacman.d/mirrorlist.bak && \
rankmirrors -n 6 /etc/pacman.d/mirrorlist.bak > /etc/pacman.d/mirrorlist && \
pacman -Syyu --noconfirm && \
pacman -S zathura zathura-pdf-mupdf zathura-djvu zathura-cb zathura-ps --noconfirm && \
pacman -S xorg-apps --noconfirm && mkdir /books && mkdir -p /root/.config/zathura

VOLUME /tmp/.X11-unix/X0:/tmp/.X11-unix/X0
VOLUME $HOME/.config/zathura:/root/.config/zathura

CMD ["bash", "-c", "zathura"]