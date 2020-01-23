# docker run -it --security-opt seccomp:unconfined -v `pwd`:/src -v `pwd`/out:/opt/shv  <img> /src/build-docker.sh

FROM debian:buster

LABEL maintainer "Milan Dunghubel <dunghubel@elektroline.cz>"

#ENV HOME /root
#ENV DEBIAN_FRONTEND noninteractive
ENV TERM=xterm

RUN apt-get update
RUN apt-get -qqy install build-essential git devscripts libfontconfig1 wget cmake

RUN echo "deb http://shv.elektroline.cz/repo/ buster main non-free" > /etc/apt/sources.list.d/elektroline.list
RUN wget -O - http://shv.elektroline.cz/repo/archive.key | apt-key add -

RUN apt-get update


RUN apt-get -qqy install libglib2.0-0 mesa-common-dev libglu1-mesa-dev libxml2-dev libpulse-dev
RUN apt-get -qqy install qt513-dev
ENV PATH="/opt/qt513/bin:/opt/qt513/lib/qt5/bin:$PATH"
RUN apt-get -qqy install libboost-filesystem-dev libboost-program-options-dev libboost-system-dev libboost-thread-dev libmbedtls-dev libssh2-1-dev libfuse-dev libvncserver-dev

WORKDIR /build


