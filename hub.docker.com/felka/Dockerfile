FROM ubuntu:14.04

MAINTAINER Felka Chang <felka_chang@htc.com>

RUN dpkg --add-architecture i386 && apt-get -y update && apt-get install -y openjdk-7-jdk \
    Python findbugs daemon ssh davfs2 libneon27 ant \
    maven ntp ntpdate gawk groovy gradle imagemagick \
    libc6:i386 libstdc++6:i386 \
    bison g++-multilib git gperf libxml2-utils make python-networkx zlib1g-dev:i386 zip \
    gnupg flex build-essential \
    curl libc6-dev libncurses5-dev:i386 x11proto-core-dev \
    libx11-dev:i386 libreadline6-dev:i386 libgl1-mesa-glx:i386 \
    libgl1-mesa-dev mingw32 tofrodos \
    python-markdown xsltproc \
    gcc g++ gcc-multilib g++ g++-4.8-multilib g++-4.8 gcc-4.8 cpp cpp-4.8 \
    && rm -rf /var/lib/apt/lists/*

