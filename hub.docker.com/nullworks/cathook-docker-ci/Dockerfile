FROM ubuntu:18.04
RUN dpkg --add-architecture i386
RUN apt-get update - && apt-get install -y -qq software-properties-common
RUN add-apt-repository ppa:ubuntu-toolchain-r/test
RUN apt-get update -qq && apt-get install -y -qq g++-8 gcc-8 g++-8-multilib gcc-8-multilib git software-properties-common libssl-dev:i386 libboost-all-dev libc6-dev:i386 gdb libsdl2-dev libglew-dev:i386 libglew-dev libfreetype6-dev libfreetype6-dev:i386 cmake libpng-dev libssl-dev cmake rsync make && apt-get autoremove && apt-get clean
