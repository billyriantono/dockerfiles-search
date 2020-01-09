FROM ubuntu:16.04
WORKDIR /source

ADD . /source

RUN apt update && \
    apt upgrade -y && \
    apt install -y \
      build-essential \
      git \
      bzip2 \
      curl \
      openssh-client \
      wget && \
    apt clean && \
    cd /opt && \
    wget https://developer.arm.com/-/media/Files/downloads/gnu-rm/6-2016q4/gcc-arm-none-eabi-6_2-2016q4-20161216-linux.tar.bz2 && \
    tar -xjf *.bz2 && \
    rm *.bz2 && \
    mv gcc-arm-none* gcc-arm-none-eabi

ENV PATH "/opt/gcc-arm-none-eabi/bin:$PATH"
