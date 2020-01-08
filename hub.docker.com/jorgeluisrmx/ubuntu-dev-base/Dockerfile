######################################################

# Dockerfile to build ubuntu:14.04 + C/C++ Python

# dev libs. Aditionaly includes some CLI and GUI tools

######################################################

# From inside this folder
# docker build -t jorgeluisrmx/ubuntu-dev-base
# From DockerHub
# docker pull jorgeluisrmx/ubuntu-dev-base
# Basic run
# docker run -it jorgeluisrmx/ubuntu-dev-base /bin/bash


FROM ubuntu:14.04
MAINTAINER jorgeluisrmx "jorgeluisrmx@gmail.com"

# Install basic libs
RUN apt-get update

RUN apt-get install -y \
    build-essential \
    gfortran \
    g++ \
    cmake \
    software-properties-common

RUN apt-get install -y \
    libatlas-base-dev \
    libboost-all-dev \
    libflann-dev \
    libgsl0-dev \
    libeigen3-dev \
    libgoogle-perftools-dev

RUN apt-get install -y \
    libfreetype6-dev \
    libxft-dev \
    python-dev \
    python-pip

# Install Python libs
RUN pip install numpy
RUN pip install scipy
RUN pip install matplotlib
RUN pip install pandas
RUN pip install tornado

# Intall some basic GUI libs
RUN apt-get install -y \
        dbus-x11 dmz-cursor-theme fonts-dejavu fonts-liberation hicolor-icon-theme \
        libgtk2.0-0 libdbus-glib-1-2 libxt6 libexif12 \
        libgl1-mesa-glx libgl1-mesa-dri

RUN update-locale LC_MESSAGES=POSIX

# Install some sound libs
RUN apt-get install -y \
    pulseaudio \
    libcanberra-gtk3-0 \
    libcanberra-gtk-module \
    libcanberra-gtk3-module \
    libasound2

# Install some basic CLI tools
RUN apt-get install -y \
    nano \
    wget \
    git \
    xz-utils \
    file \
    locales

RUN update-locale LANG=C.UTF-8

# Intall some basic GUI tools
RUN apt-get install -y \
    terminator

# Cleaning the environment
RUN apt-get clean autoclean

RUN apt-get autoremove -y
