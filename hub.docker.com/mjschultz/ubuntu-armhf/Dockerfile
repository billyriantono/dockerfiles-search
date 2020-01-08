FROM ubuntu:trusty
MAINTAINER Michael J. Schultz <mjschultz@gmail.com>

# Add the appropriate archs and where to get packages from
RUN dpkg --add-architecture i386
RUN dpkg --add-architecture armhf
COPY arm.list /etc/apt/sources.list.d/arm.list

RUN apt-get update -o APT::Architectures="amd64,i386" && apt-get install -y \
    git \
    git-core \
    build-essential \
    gcc-multilib \
    rpm \
    snmp \
    ruby-full \
    rbenv \
    ruby-build \
    python2.7 \
    python \
    python-dev \
    python-pip
RUN apt-get install --assume-yes gcc-arm-linux-gnueabihf
RUN gem install fpm && rbenv rehash

ENTRYPOINT ["/bin/bash"]
