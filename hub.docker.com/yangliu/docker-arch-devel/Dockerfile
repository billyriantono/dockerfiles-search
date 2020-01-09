FROM yangliu/arch-base:2015.06.01
MAINTAINER yangliu <i@yangliu.name>

COPY install_yaourt.sh /root/

# initilize
RUN pacman -Sy --needed --noconfirm base-devel git rsync vim \
    && pacman -Scc --noconfirm \
    && chmod +x /root/install_yaourt.sh \
    && /bin/bash /root/install_yaourt.sh

# Set Environment Varibles

ENV HOME /root