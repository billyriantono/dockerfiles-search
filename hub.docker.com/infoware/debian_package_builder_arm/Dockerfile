FROM debian

RUN apt-get update && apt-get install -y gcc-arm-linux-gnueabihf g++-arm-linux-gnueabihf build-essential devscripts cmake debhelper dh-systemd dh-exec pkg-config libboost-all-dev
#RUN apt-get update && apt-get install libcurl3
RUN dpkg --add-architecture armhf
RUN cat /etc/apt/sources.list && ARM_SOURCES='deb [arch=armhf,amd64] http://deb.debian.org/debian stretch main\ndeb [arch=armhf,amd64] http://deb.debian.org/debian stretch-updates main\ndeb [arch=armhf,amd64] http://security.debian.org/debian-security stretch/updates main' && echo "$ARM_SOURCES" && echo "$ARM_SOURCES" > /etc/apt/sources.list
RUN apt-get update && apt-get install -y libasound2-dev:armhf libgles2-mesa-dev:armhf
RUN apt-get install -y libcurl4-openssl-dev:armhf