# Fonte(s) de inspiração:
#	- https://dzone.com/articles/docker-x11-client-via-ssh
#	- https://gist.github.com/eddiejaoude/0076739fe610189581d0

FROM centos:7

MAINTAINER Filipe dos Santos Nascimento <filipef9@gmail.com>

ENV FIREFOX_VERSION=54.0b9 FIREFOX_LANGUANGE=pt-BR

RUN \
	# Install some tools
	yum update -y &&\
	yum install -y wget \
		bzip2 \
		unzip \
		xorg-x11-server-Xvfb \
		xorg-x11-twm \
		xterm \
		xorg-x11-font \
		dejavu-sans-fonts \
		dejavu-serif-fonts \
		xdotool \
		libXrender \
		libXt \
		alsa-lib \
		gtk2-devel \
		libcanberra-gtk2 \
		PackageKit-gtk3-module &&\

	yum clean all &&\

	cd &&\
	wget https://ftp.mozilla.org/pub/firefox/releases/${FIREFOX_VERSION}/linux-x86_64/${FIREFOX_LANGUANGE}/firefox-${FIREFOX_VERSION}.tar.bz2 &&\
	tar jxf firefox-*.tar.bz2 &&\
	rm -f firefox-*.tar.bz2

ADD install-addons.sh /root/firefox/

VOLUME ["/firefox_extensions"]

CMD \
	chmod +x /root/firefox/install-addons.sh &&\
	/root/firefox/install-addons.sh &&\
	/root/firefox/firefox-bin --no-remote
