FROM ubuntu:cosmic
MAINTAINER Oscar Prieto <oprietop@uoc.edu>

RUN apt-get update && apt-get install --no-install-recommends -y build-essential \
    gcc \
    unzip \
    wget \
    zip \
    gcc-avr \
    binutils-avr \
    avr-libc \
    dfu-programmer \
    dfu-util \
    gcc-arm-none-eabi \
    binutils-arm-none-eabi \
    libnewlib-arm-none-eabi \
    git \
    software-properties-common \
    avrdude \
    libusb-dev \
    && rm -rf /var/lib/apt/lists/*

ENV keyboard=xd75:default

VOLUME /qmk
WORKDIR /qmk
CMD make git-submodule; make clean; make ${keyboard}
