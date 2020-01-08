FROM debian:stretch

RUN apt-get update && apt-get -y install \
    ca-certificates \
    curl \
    gosu \
    git gcc xz-utils sudo \
    pkg-config libusb-1.0-0-dev vim openssh-client \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*

WORKDIR /root
RUN curl -L -o pi_tools.tar.gz https://github.com/raspberrypi/tools/tarball/master
#COPY rust-1.33.0-arm-unknown-linux-gnueabihf.tar /root/
#COPY rust-1.33.0-i686-unknown-linux-gnu.tar /root/
