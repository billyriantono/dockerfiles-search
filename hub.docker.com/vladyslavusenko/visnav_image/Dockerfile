FROM ubuntu:18.04

RUN apt-get update && apt-get install -y wget gnupg

RUN wget -O - https://apt.llvm.org/llvm-snapshot.gpg.key| apt-key add -
RUN echo "deb http://apt.llvm.org/bionic/ llvm-toolchain-bionic-9 main" > /etc/apt/sources.list.d/llvm9.list

RUN apt-get update && DEBIAN_FRONTEND=noninteractive apt-get install -y cmake git libtbb-dev libeigen3-dev libglew-dev ccache libjpeg-dev libpng-dev openssh-client liblz4-dev libbz2-dev libboost-regex-dev libboost-filesystem-dev libboost-date-time-dev libboost-program-options-dev libopencv-dev libpython2.7-dev libgtest-dev gfortran libc++-dev libgoogle-glog-dev libatlas-base-dev libsuitesparse-dev wget clang-9 clang-format
