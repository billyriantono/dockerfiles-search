FROM microsoft/dotnet:3.0-sdk-bionic

COPY ./sources.list /etc/apt/sources.list
RUN dpkg --add-architecture amd64
RUN dpkg --add-architecture arm64
RUN dpkg --add-architecture armhf
RUN dpkg --add-architecture i386
RUN apt-get update
RUN apt-get full-upgrade -y
RUN apt-get install -y \
    autoconf \
    automake \
    build-essential \
    clang \
    cmake \
    crossbuild-essential-arm64 \
    crossbuild-essential-armhf \
    g++-i686-linux-gnu \
    gcc-i686-linux-gnu \
    git \
    libtool \
    llvm \
    make \
    pkg-config
