FROM debian:jessie

LABEL maintainer="Alexis Pereda <alexis@pereda.fr>"
LABEL version="1.0"
LABEL description="toolchain for Debian jessie i386"

RUN echo>/etc/apt/sources.list.d/jessie-backports.list 'deb http://deb.debian.org/debian jessie-backports main'
RUN  dpkg --add-architecture i386 \
	&& apt update \
	&& apt install -y --no-install-recommends --no-install-suggests \
		make git catch gcc:i386 g++:i386 \
	&& apt install -y --no-install-recommends --no-install-suggests -tjessie-backports \
		cmake \
	&& rm -rf /var/lib/apt/lists/*
