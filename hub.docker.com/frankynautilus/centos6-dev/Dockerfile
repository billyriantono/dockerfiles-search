FROM centos:centos6.9

# --> gcc
# https://gcc.gnu.org/mirrors.html
ENV GCC_MIRROR https://mirror-hk.koddos.net/gnu

ENV GCC_VERSION 4.9.2

# wget for download_prerequisites
# gcc & gcc-c++ for make gcc 
RUN yum install -y wget gcc gcc-c++

RUN curl -O ${GCC_MIRROR}/gcc/gcc-${GCC_VERSION}/gcc-${GCC_VERSION}.tar.bz2

RUN tar -xjvf gcc-${GCC_VERSION}.tar.bz2
RUN cd gcc-${GCC_VERSION}; ./contrib/download_prerequisites

RUN mkdir -p gcc-${GCC_VERSION}/build; cd gcc-${GCC_VERSION}/build; ../configure --disable-multilib --enable-languages=c,c++
RUN cd gcc-${GCC_VERSION}/build; make -j "$(nproc)"
RUN cd gcc-${GCC_VERSION}/build; make install-strip

RUN cp /usr/local/lib64/libstdc++.so.6.0.20 /usr/lib64/libstdc++.so.6.0.20
RUN rm -f /usr/lib64/libstdc++.so.6
RUN ln -s /usr/lib64/libstdc++.so.6.0.20 /usr/lib64/libstdc++.so.6

RUN rm -rf gcc-${GCC_VERSION}; rm gcc-${GCC_VERSION}.tar.bz2

RUN yum remove -y gcc
# <-- gcc

# --> cmake
# MAJOR.MINOR
ENV CMAKE_VERSION_MINOR 3.12
# MAJOR.MINOR.PATCH
ENV CMAKE_VERSION_PATCH 3.12.0

RUN curl -O https://cmake.org/files/v${CMAKE_VERSION_MINOR}/cmake-${CMAKE_VERSION_PATCH}.tar.gz

RUN tar -xzvf cmake-${CMAKE_VERSION_PATCH}.tar.gz
RUN cd cmake-${CMAKE_VERSION_PATCH}; ./bootstrap --prefix=/usr/local

RUN cd cmake-${CMAKE_VERSION_PATCH}; make -j "$(nproc)"
RUN cd cmake-${CMAKE_VERSION_PATCH}; make install

RUN rm -rf cd cmake-${CMAKE_VERSION_PATCH}; rm cmake-${CMAKE_VERSION_PATCH}.tar.gz
# <-- cmake

# --> git
RUN yum install -y http://opensource.wandisco.com/centos/6/git/x86_64/wandisco-git-release-6-1.noarch.rpm
RUN yum install -y git
# <-- git
