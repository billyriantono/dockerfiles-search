FROM ubuntu:14.04

ENV DEBIAN_FRONTEND noninteractive

RUN set -x &&\
	dpkg --add-architecture i386 &&\
	apt-get update -yq

RUN set -x &&\
	apt-get install -yq libc6:i386 make wget libusb-1.0.0

RUN set -x &&\
	apt-get install -yq python3-pip &&\
	pip3 install pyserial &&\
	pip3 install pyftdi &&\
	apt-get autoremove -yq python3-pip

#RUN set -x &&\
#	useradd -m user &&\
#	cd /home/user &&\
#	sudo -u user wget 'https://mono-wireless.com/download/SDK/MWSDK_201805/MWSDK_Linux-i386_201805.tgz'
#
#RUN set -x &&\
#	cd /home/user &&\
#	sudo -u user tar xfz MWSDK_Linux-i386_201805.tgz

RUN set -x &&\
	mkdir -p /opt/mono-wireless &&\
	cd /opt/mono-wireless &&\
	wget 'https://mono-wireless.com/download/SDK/MWSDK_201805/MWSDK_Linux-i386_201805.tgz'

RUN set -x &&\
	cd /opt/mono-wireless &&\
	tar xfz MWSDK_Linux-i386_201805.tgz

CMD bash

