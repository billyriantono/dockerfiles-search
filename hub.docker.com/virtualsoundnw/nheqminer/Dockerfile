FROM ubuntu:xenial

MAINTAINER Asher Dawes <asher.dawes@gmail.com>

ENV DEBIAN_FRONTEND noninteractive

WORKDIR /usr/include/

ENV BOOST_VERSION=1.66
ENV BOOST_VERSION_=1.66_
ENV BOOST_ROOT=/usr/include/boost

RUN apt-get -qq update && apt-get install -q -y software-properties-common python-software-properties
RUN add-apt-repository ppa:ubuntu-toolchain-r/test -y
RUN apt-get -qq update && apt-get install -qy g++-6 gcc git wget

RUN update-alternatives --install /usr/bin/g++ g++ /usr/bin/g++-6 90

RUN wget --no-check-certificate --max-redirect 3 https://sourceforge.net/projects/boost/files/boost/1.66.0/boost_1_66_0.tar.gz


RUN mkdir -p /usr/include/boost && tar zxf boost_1_66_0.tar.gz -C /usr/include/boost --strip-components=1

RUN echo ${BOOST_ROOT}

RUN     wget https://developer.nvidia.com/compute/cuda/9.2/Prod2/local_installers/cuda-repo-ubuntu1604-9-2-local_9.2.148-1_amd64 && \
        dpkg -i cuda-repo-ubuntu1604-9-2-local_9.2.148-1_amd64 && \
        apt-get update && \
        apt-key add /var/cuda-repo-9-2-local/7fa2af80.pub && \
        apt-get -y --allow-unauthenticated install cuda && \
        rm -rf /var/lib/apt/lists/*

ENV LIBRARY_PATH /usr/local/cuda/lib64/stubs

ENTRYPOINT /bin/bash
