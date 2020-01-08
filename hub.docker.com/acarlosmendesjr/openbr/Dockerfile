FROM ubuntu:16.04

RUN apt-get update -y && \
    apt-get install -y \
      build-essential \
      wget \
      unzip

RUN apt-get install cmake cmake-curses-gui -y

WORKDIR /tmp/downloads

RUN wget -O opencv-2.4.11.zip http://sourceforge.net/projects/opencvlibrary/files/opencv-unix/2.4.11/opencv-2.4.11.zip/download

RUN unzip opencv-2.4.11.zip && \
      cd opencv-2.4.11 && \
      mkdir build && \
      cd build && \
      cmake -DCMAKE_BUILD_TYPE=Release .. && \
      make -j4 && \
      make install && \
      cd ../.. && \
      rm -rf opencv-2.4.11*

RUN apt-get install -y git qt5-default libqt5svg5-dev qtcreator

RUN git clone https://github.com/biometrics/openbr.git && \
      cd openbr && \
      git checkout v1.1.0 && \
      git submodule init && \
      git submodule update

RUN cd openbr && mkdir build && \
      cd build && \
      cmake -DCMAKE_BUILD_TYPE=Release .. && \
      make -j4 && \
      make install && \
      cd ../.. && \
      rm -rf openbr*
      
