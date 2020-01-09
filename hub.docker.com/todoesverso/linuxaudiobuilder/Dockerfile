FROM ubuntu:18.04

LABEL maintainer=todoesverso@gmail.com

ENV DEBIAN_FRONTEND noninteractive

RUN apt update && apt install --no-install-recommends -y git cmake g++ \
      build-essential qtbase5-dev qtbase5-private-dev \
      libqt5x11extras5-dev libsndfile1-dev libfftw3-dev \
      libjack-dev libasound2-dev libfluidsynth-dev \
      libfltk1.3-dev libsamplerate0-dev libxcb1-dev \
      libxcb-keysyms1-dev libgig-dev libsndio-dev \
      libxcb-util-dev libstk0-dev libmp3lame-dev \
      libsdl2-dev libsoundio-dev portaudio19-dev \
      liblist-moreutils-perl libxml-libxml-perl \
      wget stk software-properties-common python \
      libboost-all-dev libglibmm-2.4-dev \
      libcurl4-openssl-dev libarchive-dev liblo-dev \
      libtag-extras-dev libtaglib-cil-dev vamp-plugin-sdk \
      librubberband-dev libaubio-dev libusb-1.0-0-dev \
      libpangomm-1.4-dev libcwiid-dev lv2-dev \
      libserd-dev libsord-dev libsratom-dev liblilv-dev \
      libsuil-dev libxml2-dev libgtkmm-2.4-dev \
      gcc-multilib g++-multilib libqt5x11extras5-dev qtbase5-private-dev \
      libxcb-util0-dev libxcb-keysyms1-dev wine-stable libwine-dev \
      fluid \
      && rm -rf /var/lib/apt/lists/*

# These libraries generate dependecy conficts
RUN apt update && apt --no-install-recommends install -y liblrdf0-dev \
      && rm -rf /var/lib/apt/lists/*

RUN dpkg --add-architecture i386
RUN apt update && apt install --no-install-recommends -y libwine-dev:i386\
      && rm -rf /var/lib/apt/lists/*

RUN wget https://launchpad.net/~kxstudio-debian/+archive/kxstudio/+files/kxstudio-repos_9.5.1~kxstudio3_all.deb
RUN dpkg -i kxstudio-repos_9.5.1~kxstudio3_all.deb
RUN apt-get update && apt-get install -y carla-git \
      && rm -rf /var/lib/apt/lists/*
