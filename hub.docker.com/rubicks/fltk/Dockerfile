# FLTK/Dockerfile

FROM ubuntu
MAINTAINER rubicks

RUN dpkg --add-architecture i386 && \
    apt-get -y update            && \
    apt-get -y dist-upgrade      && \
    apt-get -y autoremove        && \
    apt-get -y autoclean         && \
    apt-get -y install   \
      autoconf           \
      autoconf-archive   \
      automake           \
      g++                \
      git                \
      libX11-dev         \
      libfontconfig1-dev \
      libglu1-mesa-dev   \
      libice-dev         \
      libtool            \
      libx11-dev         \
      libxcursor-dev     \
      libxext-dev        \
      libxft-dev         \
      libxi-dev          \
      libxinerama-dev    \
      libxrender-dev     \
      make               \
      man                \
      mesa-common-dev    \
      mingw32            \
      mingw32-binutils   \
      mingw32-runtime    \
      wine
  
RUN useradd luser
WORKDIR /home/luser
ADD . /home/luser

CMD /bin/bash              \
      ./autogen.sh         \
      &&                   \
      ./configure          \
        --enable-localjpeg \
        --enable-localpng  \
        --enable-localzlib \
      &&                   \
      make                 \
      &&                   \
      make install
