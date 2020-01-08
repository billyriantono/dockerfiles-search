FROM ivs0/b-ros
RUN apt-get update \
    && apt-get -y install libopencv-dev build-essential cmake git libgtk2.0-dev pkg-config python-dev python-numpy libdc1394-22 libdc1394-22-dev libjpeg-dev libpng12-dev libtiff4-dev libjasper-dev libavcodec-dev libavformat-dev libswscale-dev libxine-dev libgstreamer0.10-dev libgstreamer-plugins-base0.10-dev libv4l-dev libtbb-dev libqt4-dev libmp3lame-dev libopencore-amrnb-dev libopencore-amrwb-dev libtheora-dev libvorbis-dev libxvidcore-dev x264 v4l-utils unzip gcc g++

RUN mkdir /opencv && cd /opencv \
    && wget https://github.com/Itseez/opencv/archive/3.0.0.zip -O opencv-3.0.0.zip \
    && unzip opencv-3.0.0.zip \
    && mkdir /opencv/opencv-3.0.0/build && cd /opencv/opencv-3.0.0/build \
    && cmake -D CMAKE_BUILD_TYPE=RELEASE -D CMAKE_INSTALL_PREFIX=/usr/local -D WITH_TBB=ON -D WITH_V4L=ON \
        -D WITH_QT=ON -D WITH_OPENGL=ON .. \
    && make -j 2 && make install && rm -R /opencv

