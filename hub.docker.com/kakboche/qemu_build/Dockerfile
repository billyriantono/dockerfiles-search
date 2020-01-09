FROM ubuntu:18.04
RUN echo "deb-src http://archive.ubuntu.com/ubuntu/ bionic main restricted" >> /etc/apt/sources.list
RUN echo "deb-src http://archive.ubuntu.com/ubuntu/ bionic-updates main restricted" >> /etc/apt/sources.list
RUN apt-get update && apt-get -y build-dep qemu
RUN apt-get update && apt-get -y install \
    build-essential \
    curl \
    devscripts \
    dh-make \
    libfdt-dev \
    libfdt1 \
    libncursesw5-dev \
    lintian \
    python3-dev
RUN mkdir /src
