FROM debian:unstable
RUN apt-get update && apt-get install -y \
        curl \
        git \
        build-essential \
        g++ \
        clang \
        libc++-dev \
        libc++abi-dev \
        gdb \
        ninja-build \
        ccache \
        python3 \
        python3-pip \
    && pip3 install --force Cheetah3 pyparsing
RUN curl https://github.com/Kitware/CMake/releases/download/v3.16.0/cmake-3.16.0-Linux-x86_64.sh -L > cmake.sh && \
	sh ./cmake.sh --skip-license --prefix=/usr/local && \
	rm cmake.sh
