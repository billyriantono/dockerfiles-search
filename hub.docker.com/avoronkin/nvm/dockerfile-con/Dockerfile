############################################################
# Dockerfile to build an image with OpenCV 4.0.1 and ffmpeg libraries
# Based on Debian
############################################################

FROM debian:stable-slim
MAINTAINER Ender Tekin <etekin@wisc.edu>
ENV DEBIAN_FRONTEND noninteractive
ENV OPENCV_REPO_URL git://github.com/opencv/opencv.git
ENV OPENCV_VERSION 4.0.1
#Install git, and some other image libraries that opencv needs
WORKDIR /tmp
RUN apt-get update && \
    apt-get install -y -q apt-utils build-essential cmake git pkg-config && \
    apt-get install -y -q libavformat-dev libavcodec-dev libavfilter-dev libswscale-dev && \
    apt-get install -y -q libjpeg-dev libpng-dev libtiff-dev libeigen3-dev && \
    apt-get install -y -q libtesseract-dev libgtk2.0-dev ffmpeg && \
    apt-get autoremove && \
    apt-get clean
# Clone and build OpenCV
RUN cd /tmp && \
    git clone --depth 1 --branch $OPENCV_VERSION $OPENCV_REPO_URL && \
    cd opencv && \
    mkdir build && \
    cd build && \
    cmake -D CMAKE_BUILD_TYPE=RELEASE \
	-D CMAKE_INSTALL_PREFIX=/usr/local \
    -D ENABLE_CXX11=ON \
    -D WITH_GSTREAMER=OFF \
    -D BUILD_opencv_java=OFF \
    -D BUILD_opencv_python=OFF \
    -D WITH_CUDA=OFF \
    .. && \
    make -j$(nproc) && \
    make install && \
    cd /tmp && \
    rm -rf opencv 
