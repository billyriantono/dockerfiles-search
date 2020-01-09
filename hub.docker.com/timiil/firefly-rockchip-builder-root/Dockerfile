FROM ubuntu:16.04
LABEL maintainer "timiil <timiil@163.com>"

RUN apt-get update -y && \
    apt-get upgrade -y && \
    apt-get install -y git gcc-arm-linux-gnueabihf u-boot-tools device-tree-compiler mtools \
parted libudev-dev libusb-1.0-0-dev python-linaro-image-tools linaro-image-tools libssl-dev \
autotools-dev libsigsegv2 m4 libdrm-dev curl sed make binutils build-essential gcc g++ bash \
patch gzip bzip2 perl tar cpio python unzip rsync file bc wget libncurses5 libglib2.0-dev openssh-client lib32stdc++6  \
nano repo \
    gcc-arm-linux-gnueabihf \
gcc-aarch64-linux-gnu device-tree-compiler lzop libncurses5-dev \
libssl1.0.0 libssl-dev 

RUN mkdir -p /src && \
    cd /src && \
    git clone https://github.com/FireflyTeam/repo.git && \
    git config --global user.name "docker" && \
    git config --global user.email "" && \
    git config --global color.status "true"
