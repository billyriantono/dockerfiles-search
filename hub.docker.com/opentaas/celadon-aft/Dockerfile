#Source from Base Image
FROM ubuntu:16.04

LABEL version="1.0"
LABEL description="celadon AFT Base Image"

ENV ACS_EXECUTION_CONFIG_PATH=/dist/ACS/acs_test_suites

RUN apt-get update && apt-get install -y \
    wget \
    zip \
    unzip \
    openssh-server \
    curl \
    python \
    python-pip \
    vim \
    android-tools-adb \
    git

#installing tools for build ffmpeg
RUN apt-get install -y \
    automake \
    autoconf \
    libtool \
    gcc \
    g++ \
    build-essential \
    checkinstall \
    libopencore-amrwb-dev \
    libtheora-dev \
    libvdpau-dev \
    libvorbis-dev \
    libxvidcore-dev \
    lame \
    libva-dev \
    libvpx-dev \
    yasm \
    zlib1g-dev \
    libx264-dev \
    librtmp-dev \
    libfdk-aac-dev \
    fdkaac \
    udev

RUN pip install requests
RUN pip install psutil
RUN pip install pyserial
RUN pip install lxml
RUN pip install pyyaml
RUN pip install tzlocal
RUN pip install uiautomator
RUN pip install arrow
RUN pip install unittest2

RUN echo -e "# Intel vendor ID for ADB\nSUBSYSTEM==\"usb\", ATTRS{idVendor}==\"8087\", MODE=\"0666\"" > 51-android.rules \
    && mv 51-android.rules /etc/udev/rules.d/ \
    && service udev restart

RUN echo "************************************** install x264 start *****************************" \
    && git clone https://git.videolan.org/git/x264.git \
    && cd x264 \
    && ./configure --enable-shared --enable-static --disable-asm --prefix=/usr/local && make && make install \
    && ldconfig \
    && cd .. && rm -rf x264 \
    && echo "************************************** install x264 end *******************************"

RUN echo "************************************* install ffmpeg start ***************************" \
    && git clone https://git.ffmpeg.org/ffmpeg.git \
    && cd ffmpeg \
    && ./configure --prefix=/usr/local --enable-libx264 --enable-libfdk-aac --enable-libvpx --enable-libvorbis --enable-shared --enable-gpl --enable-version3 --enable-nonfree \
    && make \
    && make install \
    && ldconfig \
    && cd .. && rm -rf ffmpeg \
    && echo " ************************************* install ffmpeg end *****************************"


