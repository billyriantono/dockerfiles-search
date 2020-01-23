FROM debian:jessie
RUN apt-get update && apt-get install -y curl \
    && cp -a /etc/apt/sources.list /etc/apt/sources.list.bak \
    && echo "deb http://emdebian.org/tools/debian jessie main extra" >> /etc/apt/sources.list \
    && curl http://emdebian.org/tools/debian/emdebian-toolchain-archive.key | apt-key add - \
    && dpkg --add-architecture armel \
    && apt-get update \
    && apt-get upgrade -y \
    && apt-get install -y build-essential gdb-multiarch git vim \
        qemu qemu-user-static \
        libgcc-4.9-dev:armel libstdc++-4.9-dev:armel \
        gcc-4.9-base:armel libgcc-4.9-dev:armel \
        cpp-4.9-arm-linux-gnueabi binutils-arm-linux-gnueabi \
    && cd /root \
    && apt-get download gcc-4.9-arm-linux-gnueabi gcc-arm-linux-gnueabi \          
    && apt-get download g++-arm-linux-gnueabi g++-4.9-arm-linux-gnueabi \
    && dpkg --ignore-depends=libgcc-4.9-dev:armel -i gcc-4.9-arm-linux-gnueabi_4.9.2-10_amd64.deb \
    && dpkg --ignore-depends=libgcc-4.9-dev:armel -i gcc-arm-linux-gnueabi_4.9.2-10.1_all.deb \
    && dpkg --ignore-depends=libstdc++-4.9-dev:armel -i g++-4.9-arm-linux-gnueabi_4.9.2-10_amd64.deb \
    && dpkg --ignore-depends=libstdc++-4.9-dev:armel -i g++-arm-linux-gnueabi_4.9.2-10.1_all.deb \
    && rm /root/*.deb \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists
  
MAINTAINER XuHong, icehong@gmail.com
