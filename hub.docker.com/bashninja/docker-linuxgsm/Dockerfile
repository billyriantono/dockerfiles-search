#
# LinuxGSM Dockerfile
#
# https://github.com/GameServerManagers/LinuxGSM-Docker
#
FROM lsiobase/xenial
MAINTAINER Mike Weaver <>

# set version label
ARG BUILD_DATE
ARG VERSION
LABEL build_version="Linuxserver.io version:- ${VERSION} Build-date:- ${BUILD_DATE}"

ENV DEBIAN_FRONTEND noninteractive

## Base System
RUN dpkg --add-architecture i386 && \
	apt-get update -y && \
	apt-get install -y \
		binutils \
		mailutils \
		postfix \
		bc \
		curl \
		wget \
		file \
		bzip2 \
		gzip \
		unzip \
		xz-utils \
		libmariadb2 \
		bsdmainutils \
		python \
		util-linux \
		ca-certificates \
		tmux \
		lib32gcc1 \
		libstdc++6 \
		libstdc++6:i386 \
		libstdc++5:i386 \
		libsdl1.2debian \
		default-jdk \
		lib32tinfo5 \
		speex:i386 \
		libtbb2 \
		libcurl4-gnutls-dev:i386 \
		libtcmalloc-minimal4:i386 \
		libncurses5:i386 \
		zlib1g:i386 \
		libldap-2.4-2:i386 \
		libxrandr2:i386 \
		libglu1-mesa:i386 \
		libxtst6:i386 \
		libusb-1.0-0-dev:i386 \
		libxxf86vm1:i386 \
		libopenal1:i386 \
		libssl1.0.0:i386 \
		libgtk2.0-0:i386 \
		libdbus-glib-1-2:i386 \
		libnm-glib-dev:i386
## lgsm.sh
RUN	mkdir -p /opt/lgsm/ && \
	wget https://linuxgsm.com/dl/linuxgsm.sh -O /opt/lgsm/linuxgsm.sh && \
	chmod +x /opt/lgsm/linuxgsm.sh && \
# Cleanup
    apt-get clean -y && \
    apt-get autoremove -y && \
    rm -rfv /tmp/* /var/lib/apt/lists/* /var/tmp/* 
# need use xterm for LinuxGSM
ENV TERM=xterm

COPY root/ /

EXPOSE 1194 443 80

VOLUME /config