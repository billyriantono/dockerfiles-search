FROM ubuntu:latest
MAINTAINER Wesley Elfring <hi@wesleyelfring.nl>

RUN apt-get update -yqq \
    && apt-get install -yqq \
        bison g++-multilib git gperf libxml2-utils make python-networkx zip xz-utils \
        flex curl libncurses5-dev libssl-dev zlib1g-dev gawk minicom \
        openjdk-8-jdk \
        exfat-fuse exfat-utils device-tree-compiler liblz4-tool \
    && cd ~ \
    && git clone https://github.com/friendlyarm/prebuilts.git \
    && mkdir -p /opt/FriendlyARM/toolchain \
    && tar xf prebuilts/gcc-x64/aarch64-cortexa53-linux-gnu-6.4.tar.xz -C /opt/FriendlyARM/toolchain/ \
    # Cleanup
    && rm -r /var/lib/apt/lists/* \
    && export PATH=/opt/FriendlyARM/toolchain/6.4-aarch64/bin:$PATH \
    && export GCC_COLORS=auto

WORKDIR ~/
COPY . .
