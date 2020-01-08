FROM ubuntu:18.10
MAINTAINER Lucas Hutchinson <lucas.hutchinson@gmail.com>
LABEL Description="Image for building esp32 projects from git"
WORKDIR /work

ADD . /work
RUN mkdir -p ~/esp

RUN apt-get update && apt-get install -y git wget make libncurses-dev flex bison gperf python python-serial ccache curl cmake ninja-build python-pip
RUN pip install future pyparsing

RUN cd ~/esp && \
    wget https://dl.espressif.com/dl/xtensa-esp32-elf-linux64-1.22.0-80-g6c4433a-5.2.0.tar.gz && \
    tar -xzf xtensa-esp32-elf-linux64-1.22.0-80-g6c4433a-5.2.0.tar.gz
    
ENV PATH=$PATH:$HOME/esp/xtensa-esp32-elf/bin
