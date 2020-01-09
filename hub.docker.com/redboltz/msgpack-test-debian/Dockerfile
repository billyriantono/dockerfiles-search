FROM debian

MAINTAINER TAKATOSHI KONDO redboltz@gmail.com

RUN apt-get update
RUN apt-get install -y gcc
RUN apt-get install -y g++
RUN apt-get install -y clang
RUN apt-get install -y autoconf
RUN apt-get install -y automake
RUN apt-get install -y libtool

RUN apt-get install -y gcc-multilib lib32gcc1 libc6-i386 lib32z1-dev lib32stdc++6 g++-multilib

RUN apt-get install -y git
RUN apt-get install -y wget
RUN apt-get install -y unzip

RUN apt-get install -y make
RUN apt-get install -y cmake

RUN apt-get install -y zlib1g-dev
RUN apt-get install -y valgrind

RUN wget https://googletest.googlecode.com/files/gtest-1.7.0.zip
RUN unzip gtest-1.7.0.zip

RUN cp -r /gtest-1.7.0/include/gtest /usr/local/include

RUN cd gtest-1.7.0 && g++ src/gtest-all.cc -I. -Iinclude -c && g++ src/gtest_main.cc -I. -Iinclude -c && ar -rv libgtest.a gtest-all.o && ar -rv libgtest_main.a gtest_main.o
RUN mv /gtest-1.7.0/*.a /usr/local/lib

RUN cd gtest-1.7.0 && g++ -m32 src/gtest-all.cc -I. -Iinclude -c && g++ -m32 src/gtest_main.cc -I. -Iinclude -c && ar -rv libgtest.a gtest-all.o && ar -rv libgtest_main.a gtest_main.o
RUN mkdir /usr/local/lib32
RUN mv /gtest-1.7.0/*.a /usr/local/lib32
