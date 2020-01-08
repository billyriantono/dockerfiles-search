FROM fedora:latest

LABEL maintainer="sam.bristow@syrp.co.nz"

WORKDIR /project

RUN echo "*** Installing gcc (8) and clang (6) ***" \
  && dnf install -y wget \
  && dnf install -y bzip2 \
  && dnf install -y git \
  && dnf install -y clang \
  && dnf install -y gcc gcc-c++ \
  && dnf install -y boost-devel \
  && dnf install -y cmake \
  && dnf install -y make \
  && dnf install -y ccache \
  && dnf install -y which \
  && dnf install -y ninja-build \
  && dnf install -y python \
  && dnf install -y findutils \
  && dnf install -y clang-tools-extra \
  && dnf install -y ncurses-devel \
  && dnf install -y flex \
  && dnf install -y bison \
  && dnf install -y gperf \
  && dnf install -y dos2unix \
  && dnf install -y zip \
  && pip install pyserial

# Install the arm-none-eabi toolchain
RUN wget https://developer.arm.com/-/media/Files/downloads/gnu-rm/8-2018q4/gcc-arm-none-eabi-8-2018-q4-major-linux.tar.bz2 \
 && tar xjf gcc-arm-none-eabi-8-2018-q4-major-linux.tar.bz2 -C /usr/local \
 && rm -rf gcc-arm-none-eabi-8-2018-q4-major-linux.tar.bz2

ENV PATH=$PATH:/usr/local/gcc-arm-none-eabi-8-2018-q4-major/bin

# Install the ESP32 toolchain
RUN wget https://dl.espressif.com/dl/xtensa-esp32-elf-linux64-1.22.0-80-g6c4433a-5.2.0.tar.gz \
 && tar -xzf xtensa-esp32-elf-linux64-1.22.0-80-g6c4433a-5.2.0.tar.gz -C /usr/local \
 && rm -rf xtensa-esp32-elf-linux64-1.22.0-80-g6c4433a-5.2.0.tar.gz

ENV PATH=$PATH:/usr/local/xtensa-esp32-elf/bin
  

ENTRYPOINT [ "/bin/bash" ]
