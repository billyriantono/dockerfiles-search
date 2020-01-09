FROM ubuntu:18.04

ARG DEBIAN_FRONTEND=noninteractive
ENV DISPLAY :1

RUN apt-get update --fix-missing
RUN apt-get upgrade -y
RUN apt-get install -y software-properties-common
RUN apt-get update --fix-missing

RUN apt-get install -y build-essential
RUN apt-get install -y cmake
RUN apt-get install -y git
RUN apt-get install -y libc++-dev
RUN apt-get install -y lcov
RUN apt-get install -y cppcheck
RUN apt-get install -y doxygen
RUN apt-get install -y qt5-default
RUN apt-get install -y qtbase5-dev
RUN apt-get install -y libopencv-dev
RUN apt-get install -y libccfits-dev
RUN apt-get install -y libhdf5-dev
RUN apt-get install -y xserver-xorg-video-dummy
RUN apt-get install -y x11-apps
RUN apt-get remove -y xserver-xorg-legacy

VOLUME /tmp/.X11-unix

RUN git clone https://github.com/QuantStack/xtl.git
RUN cd xtl/ && cmake -DCMAKE_INSTALL_PREFIX=/usr && make install
RUN rm -rf xtl/

RUN git clone https://github.com/QuantStack/xtensor.git
RUN cd xtensor/ && cmake -DCMAKE_INSTALL_PREFIX=/usr && make install
RUN rm -rf xtensor/

RUN apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

COPY .utils/xorg.conf /etc/X11/xorg.conf

CMD ["/usr/bin/Xorg", "-noreset", "+extension", "GLX", "+extension", "RANDR", "+extension", "RENDER", "-logfile", "/tmp/xdummy.log", ":1" ]
