FROM ubuntu:16.04

# global environment settings
ENV HOME="/root"
ENV TERM="xterm"
ARG DEBIAN_FRONTEND="noninteractive"

# install packages
RUN \
 apt-get update && \
 apt-get install -y \
	apt-transport-https \
	binutils \
	jsvc \
	mongodb-server \
	apt-utils \
	openjdk-8-jre-headless \
	wget && \
	
# install UniFi beta
 wget -O /tmp/unifi_sysvinit_all.deb \
 	https://www.ubnt.com/downloads/unifi/5.2.2-6505992c/unifi_sysvinit_all.deb && \
 	dpkg -i /tmp/unifi_sysvinit_all.deb && \
 	apt-get install -f && \

# add s6 overlay
 wget -O /tmp/s6.tar.gz \
	https://github.com/just-containers/s6-overlay/releases/download/v1.17.2.0/s6-overlay-amd64.tar.gz && \
	tar xvf /tmp/s6.tar.gz -C / && \

# cleanup
 apt-get clean && \
 rm -rfv /tmp/* /var/lib/apt/lists/* /var/tmp/*

# add local files
COPY root/ /

ENTRYPOINT ["/init"]

# Volumes and Ports
WORKDIR /usr/lib/unifi
VOLUME /config
EXPOSE 8080 8081 8443 8843 8880
