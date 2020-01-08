FROM	ubuntu:14.04
MAINTAINER	toor-t

RUN	apt-get update && \
	apt-get install -y git && \
	cd /opt && \
	git clone https://github.com/raspberrypi/tools.git && \
	ln -sf /opt/tools/arm-bcm2708/arm-rpi-4.9.3-linux-gnueabihf/bin/* /usr/local/bin/

VOLUME	/work
WORKDIR	/work
