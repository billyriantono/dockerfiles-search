FROM ubuntu:14.04
LABEL maintainer "ashareye@aliyun.com"

COPY esp-open-sdk.zip /tmp/esp-open-sdk.zip
COPY tarballs.zip /tmp/tarballs.zip

ENV PACKAGES="make unrar-free autoconf automake libtool gcc g++ gperf \
    flex bison texinfo gawk ncurses-dev libexpat-dev python-dev python python-serial \
    sed git unzip bash help2man wget bzip2"

RUN apt-get update && \
    apt-get install -y $PACKAGES && \
    rm -rf /var/lib/apt/lists/* && \

    unzip /tmp/esp-open-sdk.zip -d / && \
    rm -rf /tmp/esp-open-sdk.zip && \
    mkdir /esp-open-sdk/crosstool-NG/.build && \
    unzip /tmp/tarballs.zip -d /esp-open-sdk/crosstool-NG/.build && \
    rm -rf /tmp/tarballs.zip && \

    useradd espuser && \
    chown -R espuser.espuser /esp-open-sdk

USER espuser

RUN cd /esp-open-sdk && make

ENV PATH /esp-open-sdk/xtensa-lx106-elf/bin/:$PATH

# TO BUILD : docker build -t ashareye/esp8266:0.2 . 