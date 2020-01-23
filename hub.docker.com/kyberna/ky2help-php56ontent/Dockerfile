FROM ubuntu:14.04

MAINTAINER Bin Du "bindu@ksimple.org"

RUN apt-get update
RUN apt-get install -y build-essential
RUN apt-get install -y curl
RUN apt-get install -y mtd-tools
RUN apt-get install -y genext2fs
RUN apt-get install -y mkcramfs
RUN apt-get install -y libxml2-dev
RUN apt-get install -y python
RUN apt-get install -y python-pip
RUN apt-get install -y bc
RUN apt-get install -y gawk
RUN apt-get install -y libgtk2.0-0
RUN apt-get install -y libsm-dev
RUN apt-get install -y git

ENV LINUX_TOOLCHAIN_PREFIX=/usr/local
ENV ARM_LINUX_TOOLCHAIN_DIR=$LINUX_TOOLCHAIN_PREFIX/linaro-multilib-2014.06-gcc4.9
ENV LINUX_TOOLCHAIN_VERSION=4.9.1
ENV LINUX_TOOLCHAIN_NAME=arm-linux-gnueabihf
ENV SYS_LIB_DIR_ARMV7=$ARM_LINUX_TOOLCHAIN_DIR/$LINUX_TOOLCHAIN_NAME/libc/lib/arm-linux-gnueabihf
ENV SYS_LIB_DIR_ARMV7_SF=$ARM_LINUX_TOOLCHAIN_DIR/$LINUX_TOOLCHAIN_NAME/libc/lib/armv7a-linux-gnueabi
ENV SYS_LIB_DIR_ARMV6=$ARM_LINUX_TOOLCHAIN_DIR/$LINUX_TOOLCHAIN_NAME/libc/lib/armv6k-linux-gnueabi
ENV CPP_LIB_DIR_ARMV7=$ARM_LINUX_TOOLCHAIN_DIR/$LINUX_TOOLCHAIN_NAME/libc/lib/arm-linux-gnueabihf
ENV CPP_LIB_DIR_ARMV7_SF=$ARM_LINUX_TOOLCHAIN_DIR/$LINUX_TOOLCHAIN_NAME/libc/lib/armv7a-linux-gnueabi
ENV CPP_LIB_DIR_ARMV6=$ARM_LINUX_TOOLCHAIN_DIR/$LINUX_TOOLCHAIN_NAME/libc/lib/armv6k-linux-gnueabi
ENV GCC_LIB_DIR_ARMV7=$ARM_LINUX_TOOLCHAIN_DIR/$LINUX_TOOLCHAIN_NAME/libc/lib/arm-linux-gnueabihf
ENV GCC_LIB_DIR_ARMV7_SF=$ARM_LINUX_TOOLCHAIN_DIR/$LINUX_TOOLCHAIN_NAME/libc/lib/armv7a-linux-gnueabi
ENV GCC_LIB_DIR_ARMV6=$ARM_LINUX_TOOLCHAIN_DIR/$LINUX_TOOLCHAIN_NAME/libc/lib/armv6k-linux-gnueabi
ENV GDBSERVER_DIR_ARMV7=$ARM_LINUX_TOOLCHAIN_DIR/$LINUX_TOOLCHAIN_NAME/debug-root/arm-linux-gnueabihf/usr/bin
ENV GDBSERVER_DIR_ARMV7_SF=$ARM_LINUX_TOOLCHAIN_DIR/$LINUX_TOOLCHAIN_NAME/debug-root/armv7a-linux-gnueabi/usr/bin
ENV GDBSERVER_DIR_ARMV6=$ARM_LINUX_TOOLCHAIN_DIR/$LINUX_TOOLCHAIN_NAME/debug-root/armv6k-linux-gnueabi/usr/bin
ENV ARM_ELF_TOOLCHAIN_DIR=$LINUX_TOOLCHAIN_PREFIX/arm-elf
ENV ARM_ELF_CROSS_COMPILE=arm-elf-
ENV ARM_ELF_VERSION=$LINUX_TOOLCHAIN_VERSION
ENV CROSS_COMPILE=$LINUX_TOOLCHAIN_NAME-
ENV TOOLCHAIN_PATH=$ARM_LINUX_TOOLCHAIN_DIR/bin
ENV PREBUILD_DIR=$LINUX_TOOLCHAIN_NAME
ENV CPP_INCLUDE_DIR=$ARM_LINUX_TOOLCHAIN_DIR/$LINUX_TOOLCHAIN_NAME/include/c++/$LINUX_TOOLCHAIN_VERSION
ENV CPP_INCLUDE_DIR_TOOLCHAIN=$ARM_LINUX_TOOLCHAIN_DIR/$LINUX_TOOLCHAIN_NAME/include/c++/$LINUX_TOOLCHAIN_VERSION/$LINUX_TOOLCHAIN_NAME
ENV GDB_DIR_ARMV7=$GDBSERVER_DIR_ARMV7
ENV GDB_DIR_ARMV6=$GDBSERVER_DIR_ARMV6

RUN         curl -O https://cmake.org/files/v3.6/cmake-3.6.1.tar.gz \
                && tar -xvf cmake-3.6.1.tar.gz
WORKDIR     cmake-3.6.1
RUN         ./bootstrap \
                && make \
                && make install

RUN ln -sf /bin/bash /bin/sh

