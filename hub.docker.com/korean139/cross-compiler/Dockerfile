FROM ubuntu:16.04

RUN dpkg --add-architecture i386 \
    && apt-get update -y \
    && apt-get install lib32z1 lib32stdc++6 -y \
    && apt-get install make -y \
    && mkdir /opt/toolchains

ADD arm-2014.05-29-arm-none-linux-gnueabi-i686-pc-linux-gnu.tar.bz2 /opt/toolchains/

ENV PATH="/opt/toolchains/arm-2014.05/bin:${PATH}"

WORKDIR /tmp

ENTRYPOINT make
