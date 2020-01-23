FROM ubuntu:18.04
LABEL maintainer="Andreas Pettersson"
ARG BUILD_PATH=home/build
RUN  mkdir -p ${BUILD_PATH}

RUN apt-get update && apt-get install -y \
    build-essential \
    git \
 && rm -rf /var/lib/apt/lists/*

# Build and install CMake
 ARG BUILD_PATH_CMAKE=${BUILD_PATH}/cmake
 ARG CMAKE_VERSION=v3.15.4
 RUN  git -C ${BUILD_PATH} clone https://gitlab.kitware.com/cmake/cmake.git 
 RUN  git -C ${BUILD_PATH_CMAKE} checkout tags/${CMAKE_VERSION}
 RUN ["/bin/bash", "-c", "cd ${BUILD_PATH_CMAKE};./bootstrap;make -j$(nproc);make install"]
 RUN rm -r ${BUILD_PATH}
 