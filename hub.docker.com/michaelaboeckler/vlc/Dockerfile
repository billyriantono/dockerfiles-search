FROM ubuntu:14.04
MAINTAINER Michaela Böckler 

ENV DEBIAN_FRONTEND noninteractive

#Install VLC 
RUN apt-get update && apt-get install -y  \
	libgl1-mesa-dri \
	libgl1-mesa-glx \
	vlc \
	&& rm -rf /var/lib/apt/lists/*

#change User to run vlc
ENV HOME /home/vlc
RUN useradd -m vlc

WORKDIR $HOME
#Copy an example video to test vlc
COPY Wildlife.wmv /opt/
USER vlc
ENTRYPOINT [ "vlc" , "/opt/Wildlife.wmv" ]

