FROM gcc:latest
MAINTAINER Stefan Schake <stschake@gmail.com>

RUN apt-get update \
    && apt-get remove --purge -y cmake \
    && apt-get install gcovr

RUN cd /opt && curl -s https://cmake.org/files/v3.7/cmake-3.7.2.tar.gz | tar -xz \
    && cd cmake* && ./bootstrap && make -j4 && make install && cd .. && rm -rf cmake*


