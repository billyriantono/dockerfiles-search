FROM ubuntu:disco

ENV DEBIAN_FRONTEND=noninteractive

RUN echo "dash dash/sh boolean false" | debconf-set-selections && dpkg-reconfigure dash

RUN apt-get update -y && apt-get dist-upgrade -y

RUN apt-get install build-essential pkg-config libarchive-tools bsdtar m4 gawk bc bison flex texinfo python3 perl libtool autoconf automake autopoint autoconf-archive gperf curl git wget mtools liblzma-dev pigz libgmp-dev libmpfr-dev libmpc-dev pixz libelf-dev libssl-dev zlib1g-dev zlib1g xz-utils -y

RUN apt-get install vim nano tree -y

RUN apt-get autoremove -y && apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*
