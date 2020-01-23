FROM ubuntu:14.04
MAINTAINER Tim <tim@coderhelps.com>

RUN apt-get update -qq && apt-get -o Dpkg::Options::="--force-confdef" -o Dpkg::Options::="--force-confold" -y dist-upgrade

RUN apt-get update && apt-get -y install build-essential curl tar pkg-config nasm git-core

WORKDIR /tmp/ffmpeg-src

ADD . /tmp/ffmpeg-src

RUN /tmp/ffmpeg-src/build.sh

VOLUME ['/toolchain/ffmpeg-static-3.1.1']
