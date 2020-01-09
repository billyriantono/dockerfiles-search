FROM ubuntu:18.04

# install build deps
RUN echo "deb http://us.archive.ubuntu.com/ubuntu/ bionic universe" >> /etc/apt/sources.list
RUN echo "deb http://cz.archive.ubuntu.com/ubuntu bionic main universe" >> /etc/apt/sources.list

RUN apt update
RUN apt-get install -y software-properties-common
RUN add-apt-repository -y ppa:ubuntu-toolchain-r/test

RUN apt-key adv --keyserver keyserver.ubuntu.com --recv-keys DD24C027
RUN add-apt-repository "deb http://jevois.usc.edu/apt bionic main"

RUN apt install apt-transport-https
RUN apt update

RUN apt install -y build-essential
RUN apt install -y gcc-6 g++-6
RUN apt install -y libboost-all-dev libjpeg-turbo8-dev autoconf libeigen3-dev
RUN apt install -y lsb lib32stdc++6

# only available for ubuntu:18.04
RUN apt install -y gcc-4.7-arm-linux-gnueabi gcc-6-arm-linux-gnueabihf g++-6-arm-linux-gnueabihf

RUN apt install -y pkg-config python-dev python-numpy python-pip
RUN apt install -y libdc1394-22 libdc1394-22-dev libjpeg-dev libpng-dev libtiff5-dev libavcodec-dev libavformat-dev
RUN apt install -y libswscale-dev libgstreamer1.0-dev libgstreamer-plugins-base1.0-dev libv4l-dev libtbb2 libtbb-dev
RUN apt install -y libfaac-dev libmp3lame-dev libopencore-amrnb-dev libopencore-amrwb-dev libtheora-dev libvorbis-dev
RUN apt install -y libxvidcore-dev x264 v4l-utils unzip python3-dev python3-numpy python3-pip libgtk-3-dev
RUN apt install -y libatlas-base-dev gfortran libturbojpeg libgles2-mesa libgles2-mesa-dev

RUN ln -s /usr/bin/arm-linux-gnueabi-gcc-4.7 /usr/bin/arm-linux-gnueabi-gcc
RUN ln -s /usr/lib/x86_64-linux-gnu/libturbojpeg.so.0.?.0 /usr/lib/x86_64-linux-gnu/libturbojpeg.so

# todo: see if gui tools are needed
RUN apt install -y qt5-default

