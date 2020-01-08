ARG VERSION=latest
FROM ubuntu:$VERSION

MAINTAINER Etienne Prud’homme <e.e.f.prudhomme@gmail.com>

ENV DEBIAN_FRONTEND=noninteractive

RUN echo 'APT::Get::Assume-Yes "true";' >> /etc/apt/apt.conf

RUN apt-get update && apt-get install \
    bash \
    build-essential \
    autoconf \
    git \
    texinfo \
    pkg-config \
    libgnutls28-dev \
    libasound2-dev \
    libacl1-dev \
    libncurses5-dev \
    libdbus-1-dev \
    libgconf2-dev \
    libgconf2-dev \
    libmagick++-dev \
    libgif-dev \
    libwebkit2gtk-4.0-dev \
    libgpm-dev \
    liblockfile-dev \
    libm17n-dev \
    libotf-dev \
    libselinux1-dev \
    libsystemd-dev \
    libxaw7-dev \
    xaw3dg-dev \
    libjansson-dev

CMD ["/bin/bash"]

