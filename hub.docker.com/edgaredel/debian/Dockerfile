# Sources: 
#   -https://registry.hub.docker.com/u/maxexcloo/debian/dockerfile/
#   -https://github.com/maxexcloo/Docker/blob/master/base/debian/Dockerfile


FROM debian:wheezy
MAINTAINER Edgar Gonzalez <edgar.gonzalez.catmed@gmail.com>
ADD etc /etc
ENV DEBIAN_FRONTEND noninteractive
RUN apt-get update && \
	apt-get upgrade -y && \
	apt-get install -y ca-certificates inotify-tools nano pwgen supervisor unrar unzip wget && \
	apt-get clean && \
	echo -n > /var/lib/apt/extended_states


RUN mkdir /config /data
RUN useradd -u 500 core
ADD config /config
RUN chmod +x /config/loop
CMD /config/loop