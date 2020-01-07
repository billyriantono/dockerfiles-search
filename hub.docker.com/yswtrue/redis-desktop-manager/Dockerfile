FROM ubuntu:xenial
MAINTAINER Benoit Galati <benoit.galati@gmail.com>

ARG DEBIAN_FRONTEND=noninteractive

RUN apt-get update && apt-get install -y git lsb-release sudo software-properties-common
RUN add-apt-repository ppa:ubuntu-toolchain-r/test -y && apt-get update && apt-get install -y gcc-4.8 g++-4.8
RUN ln -s /usr/bin/gcc-4.8 /usr/bin/gcc \
    && ln -s /usr/bin/g++-4.8 /usr/bin/g++

RUN git clone --recursive https://github.com/uglide/RedisDesktopManager.git -b 2019.0 rdm \
    && cd ./rdm/src \
    && ./configure \
    && . /opt/qt59/bin/qt59-env.sh && qmake && make \
    && make install
RUN cd /opt/redis-desktop-manager/ \
    && rm qt.conf

ENV QT_QPA_PLATFORM_PLUGIN_PATH /opt/qt59/plugins/platforms/
ENV LD_LIBRARY_PATH=/opt/qt59/lib/

CMD /opt/redis-desktop-manager/rdm
