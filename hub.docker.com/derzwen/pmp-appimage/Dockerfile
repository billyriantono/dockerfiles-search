FROM ubuntu:cosmic

ARG DEBIAN_FRONTEND=noninteractive

# Add package repositories
RUN set -e \
  && apt-get update \
  && apt-get install -y --no-install-recommends \
  	software-properties-common \
  	gpg-agent \
  	dirmngr \
  && echo deb http://ppa.launchpad.net/beineri/opt-qt-5.11.2-bionic/ubuntu bionic main | tee /etc/apt/sources.list.d/qt.list \
  && apt-key adv --keyserver keyserver.ubuntu.com --recv-keys E9977759 \
  && add-apt-repository -y ppa:git-core/ppa \
  && add-apt-repository -y ppa:pulse-eight/libcec \
  && rm -rf /var/lib/apt/lists/* \
  && rm -rf /tmp/* /var/tmp/* /var/log/*

# Install development tools and libraries
RUN set -e \
  && apt-get update \
  && apt-get install -y --no-install-recommends \
    nano \
    curl \
    wget \
    jq \
    autoconf \
    automake \
    libtool \
    libharfbuzz-dev \
    libfreetype6-dev \
    libfontconfig1-dev \
    libx11-dev \
    libxrandr-dev \
    libvdpau-dev \
    libva-dev \
    libbluray-dev \
    mesa-common-dev \
    libegl1-mesa-dev \
    yasm \
    libasound2-dev \
    libpulse-dev \
    libuchardet-dev \
    zlib1g-dev \
    libfribidi-dev \
    git \
    libgnutls28-dev \
    libgl1-mesa-dev \
    libsdl2-dev \
    cmake \
    build-essential \
    qt511base \
    qt511quickcontrols \
    qt511tools \
    qt511translations \
    qt511webchannel \
    qt511webengine \
    qt511x11extras \
    libcec4-dev \
    wayland-protocols \
    fuse \
    ccache \
    python \
  && rm -rf /var/lib/apt/lists/* \
  && rm -rf /tmp/* /var/tmp/* /var/log/*
