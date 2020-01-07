FROM ubuntu:latest

ENV DEBIAN_FRONTEND noninteractive

RUN echo "deb http://archive.ubuntu.com/ubuntu $(lsb_release -cs) multiverse" >> /etc/apt/sources.list
RUN apt-get update

RUN apt-get install -y wget
RUN apt-get install -y unzip
RUN apt-get install -y build-essential checkinstall cmake pkg-config yasm git libtiff4-dev libjpeg-dev libjasper-dev libavcodec-dev libavformat-dev libswscale-dev libdc1394-22-dev libxine-dev libgstreamer0.10-dev libgstreamer-plugins-base0.10-dev libv4l-dev libtbb-dev
WORKDIR /tmp
RUN wget https://github.com/Itseez/opencv/archive/2.4.9.zip
RUN unzip 2.4.9.zip

WORKDIR /tmp/opencv-2.4.9
RUN mkdir /tmp/opencv-2.4.9/build

WORKDIR /tmp/opencv-2.4.9/build

RUN cmake -D CMAKE_BUILD_TYPE=RELEASE -D CMAKE_INSTALL_PREFIX=/usr/local -D WITH_TBB=ON -D BUILD_NEW_PYTHON_SUPPORT=ON -D WITH_V4L=ON -D INSTALL_C_EXAMPLES=ON -D INSTALL_PYTHON_EXAMPLES=ON -D BUILD_EXAMPLES=ON -D WITH_QT=OFF -D WITH_OPENGL=ON ..
RUN make -j8
RUN make install
RUN echo "/usr/local/lib" > /etc/ld.so.conf.d/opencv.conf
RUN ldconfig

WORKDIR /
RUN rm -rf /tmp/*