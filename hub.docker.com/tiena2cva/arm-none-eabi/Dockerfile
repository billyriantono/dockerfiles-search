FROM ubuntu:latest

ARG DEBIAN_FRONTEND=noninteractive

RUN apt-get update && apt-get -y install \
    build-essential \
    cmake \
    git \
    wget
    
RUN wget -O gcc-arm-none-eabi.tar.bz2 https://developer.arm.com/-/media/Files/downloads/gnu-rm/8-2018q4/gcc-arm-none-eabi-8-2018-q4-major-linux.tar.bz2

RUN tar xvjf gcc-arm-none-eabi.tar.bz2

RUN mv gcc-arm-none-eabi-8-2018-q4-major gcc-arm-none-eabi

RUN rm gcc-arm-none-eabi.tar.bz2

ENV PATH="/gcc-arm-none-eabi/bin:${PATH}"
