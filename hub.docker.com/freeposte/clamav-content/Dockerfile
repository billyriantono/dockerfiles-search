FROM           ubuntu:trusty
#test
ENV            BR_VERSION 2014.11
RUN            DEBIAN_FRONTEND=noninteractive && apt-get update && apt-get install -y \
                    nano \
                    wget \
                    build-essential \
                    libncurses-dev \
                    rsync \
                    unzip \
                    bc \
                    gnupg \
                    python \
                    libc6-i386 \
                    language-pack-en-base
WORKDIR        /tmp
RUN            wget -nv http://buildroot.uclibc.org/downloads/buildroot-$BR_VERSION.tar.gz
RUN            tar -zxf buildroot-$BR_VERSION.tar.gz && mv buildroot-$BR_VERSION buildroot
RUN            cp -rf buildroot toolchain

ADD            ./Toolchain.conf /tmp/toolchain/.config
WORKDIR        /tmp/toolchain
RUN            make

WORKDIR        /opt
RUN            ln -s /tmp/toolchain/output/host/usr/ x86_64-buildroot-linux-uclibc

WORKDIR        /tmp/buildroot
