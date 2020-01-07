FROM ubuntu:16.04
LABEL maintainer="shkim519@kaist.ac.kr"

ENV LD_LIBRARY_PATH ${LD_LIBRARY_PATH}:/opencv/lib
ENV PKG_CONFIG_PATH ${PKG_CONFIG_PATH}:/opencv/

RUN apt-get update && \
    apt-get install -y --no-install-recommends curl build-essential checkinstall cmake pkg-config wget unzip \
                       libopencv-dev yasm libjpeg-dev libjasper-dev libavcodec-dev libavformat-dev libswscale-dev libdc1394-22-dev \
                       libv4l-dev python-dev python-numpy libtbb-dev libqt4-dev libgtk2.0-dev libmp3lame-dev libopencore-amrnb-dev \
                       libopencore-amrwb-dev libtheora-dev libvorbis-dev libxvidcore-dev x264 v4l-utils && \
\
    wget --no-check-certificate -O opencv.zip https://github.com/opencv/opencv/archive/3.4.0.zip && \
    wget --no-check-certificate -O opencv_contrib.zip https://github.com/opencv/opencv_contrib/archive/3.4.0.zip && \
    unzip opencv.zip -d / && \
    unzip opencv_contrib.zip -d / && \
    mkdir -p /opencv-3.4.0/build && \
    cd /opencv-3.4.0/build && \
    cmake -D CMAKE_BUILD_TYPE=RELEASE \
    -D CMAKE_INSTALL_PREFIX=/opencv \
    -D WITH_TBB=OFF \
    -D WITH_IPP=OFF \
    -D WITH_1394=OFF \
    -D BUILD_WITH_DEBUG_INFO=OFF \
    -D BUILD_DOCS=OFF \
    -D INSTALL_C_EXAMPLES=OFF \
    -D INSTALL_PYTHON_EXAMPLES=OFF \
    -D BUILD_EXAMPLES=OFF \
    -D BUILD_TESTS=OFF \
    -D BUILD_PERF_TESTS=OFF \
    -D OPENCV_EXTRA_MODULES_PATH=../../opencv_contrib-3.4.0/modules \
    ../ && \
\
    make -j$(cat /proc/cpuinfo | grep processor | wc -l) && \
    make install && \
    cp /opencv-3.4.0/build/unix-install/opencv.pc /opencv/opencv.pc && \
\
    ln -s /opencv/include/opencv2 /usr/local/include/opencv2 && \
    ln -s /opencv/include/opencv /usr/local/include/opencv && \
\
    ldconfig && \
\
    apt-get remove --purge --autoremove -y unzip curl build-essential wget cmake libtbb-dev libjpeg-dev && \
    apt-get clean && \
    apt-get autoclean && \
    apt-get autoremove && \
    cd / && \
    rm -rf opencv.zip opencv_contrib.zip opencv-3.4.0 opencv_contrib-3.4.0 && \
    rm -rf /var/lib/apt/lists* /tmp/* /var/tmp/*

WORKDIR /

