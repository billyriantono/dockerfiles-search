FROM fedora

MAINTAINER TAKATOSHI KONDO redboltz@gmail.com

RUN yum -y install gcc
RUN yum -y install gcc-c++
RUN yum -y install clang
RUN yum -y install autoconf
RUN yum -y install automake
RUN yum -y install libtool

RUN yum -y install glibc-devel.i686 libgcc.i686 libstdc++-devel.i686
RUN yum -y install zlib-devel.i686

RUN yum -y install git
RUN yum -y install wget
RUN yum -y install unzip

RUN yum -y install make
RUN yum -y install cmake

RUN yum -y install zlib-devel
RUN yum -y install valgrind

RUN wget https://googletest.googlecode.com/files/gtest-1.7.0.zip
RUN unzip gtest-1.7.0.zip

RUN cp -r /gtest-1.7.0/include/gtest /usr/local/include

RUN cd gtest-1.7.0 && g++ src/gtest-all.cc -I. -Iinclude -c && g++ src/gtest_main.cc -I. -Iinclude -c && ar -rv libgtest.a gtest-all.o && ar -rv libgtest_main.a gtest_main.o
RUN mv /gtest-1.7.0/*.a /usr/local/lib64

RUN cd gtest-1.7.0 && g++ -m32 src/gtest-all.cc -I. -Iinclude -c && g++ -m32 src/gtest_main.cc -I. -Iinclude -c && ar -rv libgtest.a gtest-all.o && ar -rv libgtest_main.a gtest_main.o
RUN mv /gtest-1.7.0/*.a /usr/local/lib
