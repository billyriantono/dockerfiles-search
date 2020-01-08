FROM ubuntu:14.04.5

MAINTAINER Chakkrit Termritthikun <chakkritte57@nu.ac.th>

RUN \
  apt-get -q -y update 

RUN \
  apt-get -q -y install \
  wget \
  unzip \
  libopencv-dev \
  build-essential \
  checkinstall \
  cmake \
  pkg-config \
  yasm \
  libtiff4-dev \
  libjpeg-dev \
  libjasper-dev \
  libavcodec-dev \
  libavformat-dev libswscale-dev libdc1394-22-dev libxine-dev libgstreamer0.10-dev libgstreamer-plugins-base0.10-dev libv4l-dev python-dev python-numpy libtbb-dev libqt4-dev libgtk2.0-dev \
  #libfaac-dev \
  libmp3lame-dev libopencore-amrnb-dev libopencore-amrwb-dev libtheora-dev libvorbis-dev libxvidcore-dev x264 v4l-utils \
  && apt-get upgrade -q -y  \
  && apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

RUN cd /root/ \
  && wget https://github.com/opencv/opencv/archive/2.4.13.1.zip \
  && unzip 2.4.13.1.zip \
  && rm 2.4.13.1.zip -r -f \
  && cd opencv-2.4.13.1/ \
  && mkdir release \
  && cd release \
  && cmake -D CMAKE_BUILD_TYPE=RELEASE -D CMAKE_INSTALL_PREFIX=/usr/local -D WITH_TBB=ON -D BUILD_NEW_PYTHON_SUPPORT=ON -D WITH_V4L=ON -D INSTALL_C_EXAMPLES=ON -D INSTALL_PYTHON_EXAMPLES=ON -D BUILD_EXAMPLES=ON -D WITH_QT=ON -D WITH_OPENGL=ON .. \
  && make -j8\
  && make install \
  && rm /root/opencv-2.4.13.1/ -r -f
