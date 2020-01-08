FROM ubuntu:18.04

LABEL version="18.04"
LABEL description="Ubuntu 18.04 based image with development packages"

ENV TERM xterm-256color

RUN apt-get update && \
    apt-get install -qqy --no-install-recommends \
        automake autoconf \
        bc bison bzip2 build-essential \
        cmake curl ccache cpio \
        dialog dfu-util device-tree-compiler \
        fakeroot file flex \
        gawk gcc g++ gettext git gperf \
        help2man \
        libconfuse-dev libtool-bin libexpat-dev \
        libncurses-dev libmpfr-dev libxml-parser-perl \
        lzop \
        make \
        ninja-build \
        patch pkg-config python-dev python3-dev \
        python3 python-setuptools python-serial \
        python3-setuptools python-pip python3-pip \
        python3-wheel \
        sudo \
        texinfo \
        unzip \
        wget \
        xz-utils \
        zip && \
    apt-get clean && \
    apt-get autoremove -y

# delete all the apt list files since they're big and get stale quickly
RUN rm -rf /var/lib/apt/lists/*

# vim: ts=4 sw=4 et
