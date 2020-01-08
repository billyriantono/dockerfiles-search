# Install a C++ SDK

FROM ubuntu
MAINTAINER Uilian Ries <uilianries@gmail.com>

RUN apt-get update
RUN apt-get install -y software-properties-common python-software-properties
RUN add-apt-repository ppa:ubuntu-toolchain-r/test --yes
RUN apt-add-repository "deb http://llvm.org/apt/xenial/ llvm-toolchain-xenial-3.8 main"
RUN apt-get update
RUN apt-get install -y --force-yes gcc-6 g++-6 python-pip cmake git vim valgrind doxygen cppcheck clang-3.8 lldb-3.8 clang-format-3.8 clang-tidy-3.8 lcov
RUN apt-get install -y sudo
RUN update-alternatives --install /usr/bin/gcc gcc /usr/bin/gcc-6 60 --slave /usr/bin/g++ g++ /usr/bin/g++-6
RUN pip install --upgrade pip
RUN pip install conan cmakelint cpplint

RUN groupadd docker
RUN useradd -c 'Docker user' -m -d /home/docker -s /bin/bash docker -g docker
RUN echo "docker:docker" | chpasswd && adduser docker sudo
USER docker

RUN conan install Poco/1.7.3@lasote/stable -s compiler=gcc -s compiler.version=6.1 -s compiler.libcxx=libstdc++11 --build=missing
RUN conan install Boost/1.60.0@lasote/stable -s compiler=gcc -s compiler.version=6.1 -s compiler.libcxx=libstdc++11 --build=missing
RUN conan install gtest/1.7.0@lasote/stable -s compiler=gcc -s compiler.version=6.1 -s compiler.libcxx=libstdc++11 --build=missing

ENV HOME /home/docker
ENV DEVEL $HOME/devel
RUN mkdir $DEVEL
WORKDIR $DEVEL

CMD ["bash"]
