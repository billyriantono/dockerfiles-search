FROM ubuntu:16.04

RUN apt-get update

RUN apt-get install -y -q --no-install-recommends \
        apt-utils \
        python3-dev \
        python3-pip \
        python3-setuptools \
        gcc \
        g++ \
        ninja-build


RUN pip3 install meson
RUN apt-get install -y wget

# opencv deps
RUN apt-get install -y -q --no-install-recommends \
    cmake \
    libgtk2.0-dev \
    pkg-config \
    libavcodec-dev \
    libavformat-dev \
    libswscale-dev \
    libtbb2 \
    libtbb-dev \
    libjpeg-dev \
    libpng-dev \
    libtiff-dev \
    unzip

# build OpenCV 3.2
RUN cd \
    && wget https://github.com/opencv/opencv/archive/3.2.0.zip \
    && unzip 3.2.0.zip \
    && cd opencv-3.2.0 \
    && mkdir build \
    && cd build \
    && cmake .. \
    && make -j2 \
    && make install \
    && cd \
    && rm 3.2.0.zip

# add thelocal libs to the paths
RUN ldconfig
ENV PATH="/usr/local/lib64:${PATH}"

CMD ["/bin/bash"]
