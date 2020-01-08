FROM base/devel
MAINTAINER Felix Morgner <felix.morgner@gmail.com>

RUN pacman \
 -Sy \
 --noconfirm \
 --needed \
 base-devel \
 boost \
 cmake \
 git \
 ninja \
 qt5 \
 && pacman -Scc --noconfirm
