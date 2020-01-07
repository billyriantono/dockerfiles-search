FROM ubuntu:zesty
MAINTAINER Jaroslav Ř., https://github.com/jaroslavrehorka
RUN apt-get update && \
    apt-get upgrade -y && \
    apt-get install -y  make=4.1-9.1 && \
    apt-get install -y  cmake=3.7.2-1 && \
    apt-get install -y  valgrind=1:3.12.0-1ubuntu1 && \
    apt-get install -y  clang=1:3.9-34ubuntu1 && \
    apt-get install -y  build-essential=12.1ubuntu2 && \
    apt-get clean
    