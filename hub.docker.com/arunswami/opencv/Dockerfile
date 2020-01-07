#Arunachalam 
#install on top of ubuntu 16.04 official image
FROM ubuntu:16.04

RUN apt update 
#install the dependencies of the opencv 3.2.0
RUN apt-get install -y cmake git libgtk2.0-dev pkg-config libavcodec-dev \
      libavformat-dev libswscale-dev python-dev python-numpy libtbb2 libtbb-dev \
      libjpeg-dev libpng-dev libtiff-dev libjasper-dev libdc1394-22-dev unzip

RUN apt install -y wget vim
#build and install opencv 3.2.0 
RUN cd \
    && wget https://github.com/opencv/opencv/archive/3.2.0.zip \
    && unzip 3.2.0.zip \
    && cd opencv-3.2.0 \
    && mkdir build \
    && cd build \
    && cmake -DCMAKE_BUILD_TYPE=Release -DCMAKE_INSTALL_PREFIX=/usr/local .. \
    && make -j8 \
    && make install \
    && cd \
    && rm 3.2.0.zip
WORKDIR / 
CMD ["bin/bash", "-c"]
