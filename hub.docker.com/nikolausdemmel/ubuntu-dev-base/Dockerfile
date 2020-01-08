FROM ubuntu:14.04

# non-persistent environment variables
ARG DEBIAN_FRONTEND=noninteractive

# Basic packages
RUN apt-get update && apt-get install -y \
    apt-transport-https \
    software-properties-common \
    locales

# Set the locale
RUN locale-gen en_US.UTF-8
ENV LANG en_US.UTF-8
ENV LANGUAGE en_US:en
ENV LC_ALL en_US.UTF-8

# PPAs

# gcc 5
RUN add-apt-repository -y ppa:ubuntu-toolchain-r/test

# cmake 3.2
# TODO: consider getting latest cmake from pip...
RUN add-apt-repository -y ppa:george-edison55/cmake-3.x

# upgrade packages
RUN apt-get update && apt-get upgrade -y

# Install base dependencies
RUN apt-get update && apt-get install -y \
    build-essential \
    gcc-5 \
    g++-5 \
    clang-3.9 \
    libc++-dev \
    cmake \
    pkg-config \
    wget \
    curl \
    git \
    ccache \
    aptitude

# Python
RUN apt-get update && apt-get install -y \
    python \
    python3 \
    libpython-all-dev \
    libpython3-all-dev

# Install larger libs
RUN apt-get update && apt-get install -y \
    libboost-all-dev

# Install some tools
RUN apt-get update && apt-get install -y \
    emacs \
    vim \
    cmake-curses-gui

# Install additional libs
RUN apt-get update && apt-get install -y \
    libgoogle-glog-dev

# GCC 5 default:
# update-alternatives --install /usr/bin/gcc gcc /usr/bin/gcc-5 60 --slave /usr/bin/g++ g++ /usr/bin/g++-5
