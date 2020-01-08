# Serviio docker
#
# Project forked from https://github.com/riftbit/docker-serviio
#
# VERSION               0.3
# Run with: 
#	docker run -d --rm --name serviio \
#	        -v /media/<folder>:/media \
#	        -v /opt/serviio-2.0/library:/opt/serviio/library \
#	        -v /opt/serviio-2.0/plugins:/opt/serviio/plugins \
#	        -v /opt/serviio-2.0/log:/opt/serviio/log \
#	        -p 23423:23423/tcp \
#	        -p 23424:23424/tcp \
#	        -p 8895:8895/tcp \
#	        -p 1900:1900/udp \
#	        -p 1901:1901/udp \
#	        -p 1901:1901/tcp \
#	        --net=host \
#	        jfrs/debian-serviio

FROM debian:stretch-slim

# Install Dependencies
RUN echo 'deb http://deb.debian.org/debian stretch main contrib non-free' > /etc/apt/sources.list && \
    echo 'deb http://deb.debian.org/debian stretch-updates main' >> /etc/apt/sources.list && \
    echo 'deb http://security.debian.org stretch/updates main' >> /etc/apt/sources.list && \
    apt-get update && apt-get upgrade -y 

RUN mkdir -p /usr/share/man/man1/
RUN apt-get install -y openjdk-8-jre x264 ffmpeg

RUN apt-get install -y apt-utils curl wget tar bzip2 build-essential checkinstall git libjack-jackd2-dev libvpx4 \
        libmp3lame-dev libopencore-amrnb-dev libopencore-amrwb-dev libsdl1.2-dev libtheora-dev librtmp1 openssl \
        libva-dev libvdpau-dev libvorbis-dev libx11-dev libxfixes-dev texi2html zlib1g-dev rtmpdump libfdk-aac-dev \
        libssl1.1 libssl-dev libxvidcore-dev libxvidcore4 libass-dev dcraw gnupg librtmp-dev libfdk-aac1 libvpx-dev
	
ARG SERVIIO_VERSION=2.0

# Install Serviio
CMD cd $HOME/src 
RUN curl -s http://download.serviio.org/releases/serviio-${SERVIIO_VERSION}-linux.tar.gz | tar zxf - -C . 
RUN mkdir -p /opt/serviio && \
  mv ./serviio-${SERVIIO_VERSION}/* /opt/serviio && \
  chmod +x /opt/serviio/bin/serviio.sh && \
  rm -rf $HOME/src

VOLUME ["/opt/serviio/library", "/opt/serviio/plugins", "/opt/serviio/log", "/media"]

EXPOSE 23423:23423/tcp
EXPOSE 23424:23424/tcp
EXPOSE 23425:23425/tcp
EXPOSE 8895:8895/tcp
EXPOSE 1900:1900/udp
EXPOSE 1901:1901/udp

CMD /opt/serviio/bin/serviio.sh

