#
# Minimum Docker image to build Android AOSP
#
FROM ubuntu:18.04

MAINTAINER chenchacha <chen.chenchacha@qq.com>


# Keep the dependency list as short as reasonable
RUN apt-get update && \
    apt-get install -y git gnupg flex bison gperf build-essential zip curl \
    zlib1g-dev gcc-multilib g++-multilib libc6-dev-i386 lib32ncurses5-dev \
    x11proto-core-dev libx11-dev lib32z1-dev libgl1-mesa-dev libxml2-utils \
    xsltproc unzip imagemagick python-networkx rsync bc libssl-dev && \
    apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

CMD ["/bin/bash"]
