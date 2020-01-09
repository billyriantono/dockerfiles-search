FROM ubuntu:latest
MAINTAINER Brandon@megadocker.com

RUN mkdir /gccg
WORKDIR /gccg
RUN apt-get update -y && \
apt-get install -y libsdl2-2.0-0 libsdl2-image-2.0-0 libsdl2-net-2.0-0 libsdl2-mixer-2.0-0 libsdl2-ttf-2.0-0 wget && \
wget http://gccg.sourceforge.net/modules/gccg-core-1.0.10.tgz && \
tar -xzvf gccg-core-1.0.10.tgz && \
./gccg_package install client fonts linux-i386 && \
rm gccg-core-1.0.10.tgz && \
rm -rf /var/lib/apt/lists/*