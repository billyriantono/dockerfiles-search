FROM ubuntu:18.04

ENV DEBIAN_FRONTEND=noninteractive

RUN dpkg --add-architecture i386

RUN apt-get update && \
    apt-get install -y \
    build-essential git vim wget unzip sudo \
    libc6:i386 libncurses5:i386 libstdc++6:i386 lib32z1 libbz2-1.0:i386 \
    libxrender1 libxtst6 libxi6 libfreetype6 libxft2 \
    qemu qemu-kvm libvirt-bin ubuntu-vm-builder bridge-utils libnotify4 libglu1 libqt5widgets5 openjdk-8-jdk xvfb \ 
    && apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

ADD https://dl.google.com/dl/android/studio/ide-zips/3.4.1.0/android-studio-ide-183.5522156-linux.tar.gz /opt/android-studio.tar.gz
RUN cd /opt/ && tar xvzf android-studio.tar.gz && rm android-studio.tar.gz

WORKDIR /workdir

RUN useradd -Ms /bin/bash develop && chown develop /workdir

USER develop

CMD /opt/android-studio/bin/studio.sh

