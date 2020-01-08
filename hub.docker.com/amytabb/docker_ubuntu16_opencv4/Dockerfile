FROM amytabb/docker_ubuntu16_essentials
MAINTAINER Amy Tabb

RUN git clone https://github.com/opencv/opencv.git

COPY build_opencv.sh /build_opencv.sh

WORKDIR /opencv/build 

RUN /bin/sh ./../../build_opencv.sh

WORKDIR /
#do not remove directory, because will use this image for building the contrib module as well.
