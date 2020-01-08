FROM ruby:2.5.5

RUN apt-get update && apt-get -y install build-essential cmake libgtk2.0-dev pkg-config \
                                     python-numpy python-dev libavcodec-dev libavformat-dev \
                                     libswscale-dev libjpeg-dev libpng-dev libtiff5-dev \
                                     libopencv-dev  checkinstall pkg-config \
                                     yasm libjpeg-dev libavcodec-dev \
                                     libavformat-dev libswscale-dev libdc1394-22-dev \
                                     libxine2 libgstreamer1.0-dev  libv4l-dev \
                                     libgstreamer-plugins-base1.0-dev python-dev \
                                     python-numpy libtbb-dev libqt4-dev libgtk2.0-dev \
                                     libmp3lame-dev libopencore-amrnb-dev \
                                     libopencore-amrwb-dev libtheora-dev libvorbis-dev \
                                     libxvidcore-dev x264 v4l-utils unzip


COPY opencv_install.sh ./

RUN chmod +x ./opencv_install.sh && ./opencv_install.sh && \
    rm ./opencv_install.sh
